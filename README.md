# knowledge

IF OBJECT_ID(N'dbo.alert_log', N'U') IS NOT NULL  
   DROP TABLE [dbo].[alert_log];  
GO


CREATE TABLE [dbo].[alert_log](
[id]	INT IDENTITY NOT NULL,
[correlation_id]	NVARCHAR(36) 	NOT NULL, 
[customer_id]	NVARCHAR(36) NOT NULL,
[notification_type]	NVARCHAR(36) NOT NULL,
[payload] NVARCHAR(MAX) NULL,
[duplicate]	BIT NULL,
[created]	DATETIME 	NOT NULL,
[updated]	DATETIME 	NOT NULL
)
GO

IF OBJECT_ID(N'dbo.push_message', N'U') IS NOT NULL  
   DROP TABLE [dbo].[push_message];  
GO

CREATE TABLE [dbo].[push_message](
[id]	INT IDENTITY NOT NULL,
[event_type]	NVARCHAR(36) NOT NULL,
[event_name]	NVARCHAR(255) NULL,
[event_title]	NVARCHAR(255) NULL,
[message]	NVARCHAR(255) NULL,
[click_action] NVARCHAR(36) NULL,
[created]	DATETIME 	NOT NULL,
[updated]	DATETIME 	NOT NULL,
CONSTRAINT PK_PUSH_MESSAGE PRIMARY KEY (id)

)
GO

IF OBJECT_ID(N'dbo.email_message', N'U') IS NOT NULL  
   DROP TABLE [dbo].[email_message];  
GO


CREATE TABLE [dbo].[email_message](
[id]	INT IDENTITY NOT NULL,
[subject]	NVARCHAR(36) NOT NULL,
[message]	NVARCHAR(255) NULL,
[address]	NVARCHAR(255) NULL,
[created]	DATETIME 	NOT NULL,
[updated]	DATETIME 	NOT NULL,
CONSTRAINT PK_EMAIL_MESSAGE PRIMARY KEY (id)
)
GO

IF OBJECT_ID(N'dbo.sms_message', N'U') IS NOT NULL  
   DROP TABLE [dbo].[sms_message];  
GO


CREATE TABLE [dbo].[sms_message](
[id]	INT IDENTITY NOT NULL,
[mobile_phone_number]	NVARCHAR(14) NOT NULL,
[message]	NVARCHAR(255) NULL,
[created]	DATETIME 	NOT NULL,
[updated]	DATETIME 	NOT NULL,
CONSTRAINT PK_SMS_MESSAGE PRIMARY KEY (id)

)
GO

IF OBJECT_ID(N'dbo.alert_message', N'U') IS NOT NULL  
   DROP TABLE [dbo].[alert_message];  
GO


CREATE TABLE [dbo].[alert_message](
[id]	INT IDENTITY NOT NULL,
[correlation_id]	NVARCHAR(36) 	NOT NULL, 
[customer_id]	NVARCHAR(36) NOT NULL,
[bank_number]	NVARCHAR(255) NULL,
[source_channel]	NVARCHAR(36) NULL,
[notification_type]	NVARCHAR(36) NULL,
[push_id] INT NULL,
[sms_id] INT NULL,
[email_id] INT NULL,
[created]	DATETIME 	NOT NULL,
[updated]	DATETIME 	NOT NULL,
CONSTRAINT PK_ALERT_MESSAGE PRIMARY KEY (id),
CONSTRAINT FK_PUSH_MESSAGE FOREIGN KEY (push_id) REFERENCES dbo.push_message (id),
CONSTRAINT FK_SMS_MESSAGE FOREIGN KEY (sms_id) REFERENCES dbo.sms_message (id),
CONSTRAINT FK_EMAIL_MESSAGE FOREIGN KEY (email_id) REFERENCES dbo.email_message (id),
)
GO
