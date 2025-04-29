# SOAR-EDR
# Playbook

![SOAR Workflow Diagram](./SOAR_EDR_Playbook.drawio.png)

A Security Orchestration, Automation, and Response (SOAR) system integrated with Endpoint Detection and Response (EDR) capabilities.

## Workflow Overview

### 1. Alert Ingestion
- Receives alerts from LimaCharlie EDR
- Processes through Tines automation
- Captures alert details:
  - Timestamp
  - Computer name
  - Source IP
  - Process info
  - Command line
  - File path
  - Sensor ID
  - Detection link
  - Username

### 2. Notification
- **Slack**: Instant alerts
- **Email**: Audit trail

### 3. Isolation Decision
```mermaid
graph TD
    A[Alert] --> B{Isolate machine?}
    B -->|YES| C[Initiate isolation]
    B -->|NO| D[Flag for investigation]
```
## Response Actions

| Decision | Actions |
|----------|---------|
| ✅ **YES** | • Isolate via LimaCharlie<br>• Verify isolation status<br>• Send confirmation notification |
| ❌ **NO**  | • Log decision in audit trail<br>• Create investigation ticket<br>• Notify security team |

## Integrated Components

| Component       | Purpose                                | Integration Type               |
|-----------------|----------------------------------------|--------------------------------|
| **LimaCharlie** | EDR core system for detection          | Primary detection source       |
| **Tines**       | Workflow automation and orchestration  | Playbook execution             |
| **Slack**       | Real-time alert notifications         | Communication channel          |
| **Email**       | Audit trail and documentation          | Secondary notification         |
