CREATE TABLE REMINDER (
    id                  NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,

    -- ═══════════════════════════════════════════════════════════
    -- THÔNG TIN CƠ BẢN
    -- ═══════════════════════════════════════════════════════════
    title               VARCHAR2(255) NOT NULL,              -- Tên Reminder
    reminder_type       VARCHAR2(50) NOT NULL,               -- Loại: CALL/MEETING/TASK/RENEWAL/FOLLOW_UP
    description         CLOB,                                -- Mô tả nội dung công việc
    
    -- ═══════════════════════════════════════════════════════════
    -- LIÊN KẾT MODULE CRM
    -- ═══════════════════════════════════════════════════════════
    ref_module          VARCHAR2(50),                        -- Module: DEAL/POOL/ACCOUNT/CONTACT/LEAD/MKT
    ref_id              NUMBER,                              -- ID bản ghi trong module
    
    -- ═══════════════════════════════════════════════════════════
    -- MỨC ĐỘ ƯU TIÊN (Ma trận Eisenhower)
    -- ═══════════════════════════════════════════════════════════
    is_important        NUMBER(1) DEFAULT 0,                 -- 1: Quan trọng, 0: Ít quan trọng
    is_urgent           NUMBER(1) DEFAULT 0,                 -- 1: Cần gấp, 0: Chưa cần gấp
    priority_score      NUMBER GENERATED ALWAYS AS (         -- Điểm ưu tiên tự động tính
                            is_important * 2 + is_urgent
                        ) VIRTUAL,
    
    -- ═══════════════════════════════════════════════════════════
    -- THỜI GIAN
    -- ═══════════════════════════════════════════════════════════
    due_date            TIMESTAMP,                           -- Ngày hết hạn (deadline)
    
    -- Recurring (Tần suất lặp)
    frequency           VARCHAR2(20) DEFAULT 'ONCE',         -- ONCE/DAILY/WEEKLY/MONTHLY/QUARTERLY
    recurring_end_date  TIMESTAMP,                           -- Ngày kết thúc lặp
    next_occurrence     TIMESTAMP,                           -- Lần lặp tiếp theo
    
    -- ═══════════════════════════════════════════════════════════
    -- KÊNH GỬI THÔNG BÁO
    -- ═══════════════════════════════════════════════════════════
    channels            VARCHAR2(100) DEFAULT 'EMAIL,NOTI',  -- EMAIL, NOTI, SMS
    
    -- ═══════════════════════════════════════════════════════════
    -- NGƯỜI LIÊN QUAN
    -- ═══════════════════════════════════════════════════════════
    creator_id          VARCHAR2(50) NOT NULL,               -- Người tạo
    
    -- ═══════════════════════════════════════════════════════════
    -- TRẠNG THÁI CÔNG VIỆC
    -- ═══════════════════════════════════════════════════════════
    status              VARCHAR2(20) DEFAULT 'IN_PROGRESS',  -- IN_PROGRESS/COMPLETED/OVERDUE
    completed_date      TIMESTAMP,                           -- Ngày hoàn thành
    
    -- ═══════════════════════════════════════════════════════════
    -- AUDIT
    -- ═══════════════════════════════════════════════════════════
    create_date         TIMESTAMP DEFAULT SYSTIMESTAMP,
    modified_date       TIMESTAMP,
    modified_by         VARCHAR2(50)
);

-- Constraints
ALTER TABLE REMINDER ADD CONSTRAINT chk_reminder_type
    CHECK (reminder_type IN ('CALL', 'MEETING', 'TASK', 'RENEWAL', 'FOLLOW_UP'));

ALTER TABLE REMINDER ADD CONSTRAINT chk_ref_module
    CHECK (ref_module IN ('DEAL', 'POOL', 'ACCOUNT', 'CONTACT', 'LEAD', 'MKT'));

ALTER TABLE REMINDER ADD CONSTRAINT chk_frequency
    CHECK (frequency IN ('ONCE', 'DAILY', 'WEEKLY', 'MONTHLY', 'QUARTERLY'));

ALTER TABLE REMINDER ADD CONSTRAINT chk_status
    CHECK (status IN ('IN_PROGRESS', 'COMPLETED', 'OVERDUE'));

-- Indexes
CREATE INDEX idx_reminder_status_due ON REMINDER(status, due_date);
CREATE INDEX idx_reminder_priority ON REMINDER(priority_score DESC, create_date DESC);
CREATE INDEX idx_reminder_ref ON REMINDER(ref_module, ref_id);
CREATE INDEX idx_reminder_creator ON REMINDER(creator_id);

-- Comments
COMMENT ON TABLE REMINDER IS 'Bảng chính lưu thông tin Reminder';
COMMENT ON COLUMN REMINDER.priority_score IS '3=Quan trọng+Gấp, 2=Quan trọng, 1=Gấp, 0=Thường';

CREATE TABLE REMINDER_NOTIFICATION (
    id                  NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    reminder_id         NUMBER NOT NULL,

    -- ═══════════════════════════════════════════════════════════
    -- THỜI GIAN GỬI
    -- ═══════════════════════════════════════════════════════════
    warning_interval    NUMBER NOT NULL,                     -- Số phút trước due_date
    notify_time         TIMESTAMP NOT NULL,                  -- = due_date - warning_interval
    
    -- ═══════════════════════════════════════════════════════════
    -- KÊNH GỬI (Override từ Reminder nếu cần)
    -- ═══════════════════════════════════════════════════════════
    channels            VARCHAR2(100),                       -- NULL = dùng của Reminder
    
    -- ═══════════════════════════════════════════════════════════
    -- TRẠNG THÁI GỬI
    -- ═══════════════════════════════════════════════════════════
    status              VARCHAR2(20) DEFAULT 'PENDING',      -- PENDING/SENT/FAILED/SKIPPED
    sent_time           TIMESTAMP,
    error_message       VARCHAR2(500),
    retry_count         NUMBER DEFAULT 0,
    
    -- ═══════════════════════════════════════════════════════════
    -- SNOOZE (Tạm hoãn)
    -- ═══════════════════════════════════════════════════════════
    snooze_until        TIMESTAMP,                           -- Tạm hoãn đến thời điểm này
    snooze_count        NUMBER DEFAULT 0,                    -- Số lần đã snooze
    
    -- Audit
    create_date         TIMESTAMP DEFAULT SYSTIMESTAMP,
    
    CONSTRAINT fk_notification_reminder FOREIGN KEY (reminder_id) 
        REFERENCES REMINDER(id) ON DELETE CASCADE
);

-- Index quan trọng cho Job
CREATE INDEX idx_notification_pending ON REMINDER_NOTIFICATION(status, notify_time);
CREATE INDEX idx_notification_reminder ON REMINDER_NOTIFICATION(reminder_id);

COMMENT ON COLUMN REMINDER_NOTIFICATION.warning_interval IS
    '10080=7 ngày, 1440=1 ngày, 30=30 phút';
