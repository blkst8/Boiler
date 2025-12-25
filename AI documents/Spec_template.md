# **Product Feature Specification for AI Agents**

## **Document Control**

```yaml
feature_id: "FEAT-[PRODUCT]-[NUMBER]"
feature_name: "[Clear, User-Facing Feature Name]"
version: "1.0.0"
status: "DRAFT | REVIEW | APPROVED | IN_DEVELOPMENT | COMPLETED"
created_date: "YYYY-MM-DD"
last_updated: "YYYY-MM-DD"
owner: "[Product Owner Name]"
engineering_lead: "[Tech Lead Name]"
ai_agent_ready: true
priority: "P0-CRITICAL | P1-HIGH | P2-MEDIUM | P3-LOW"
target_release: "vX.Y.Z or Sprint N"
estimated_effort: "[Story points or hours]"
```

---

## **1. Product Overview**

### 1.1 Feature Summary
**One-sentence description:**  
[What does this feature do from a user's perspective?]

**Example:** "Allow users to schedule posts for future publication with timezone support and automatic retry on failure."

### 1.2 Problem Statement

**Current State (Before):**  
[What pain point exists today? What can't users do?]

**Desired State (After):**  
[What will users be able to do with this feature?]

**Impact:**  
[How does this improve the user experience or business metrics?]

### 1.3 Success Metrics

```yaml
primary_metrics:
  - metric: "[Metric name]"
    baseline: "[Current value]"
    target: "[Target value]"
    measurement: "[How to measure]"
    timeframe: "[When to measure]"
    
  example:
    metric: "User engagement rate"
    baseline: "45%"
    target: "60%"
    measurement: "% of users who use feature weekly"
    timeframe: "30 days post-launch"

secondary_metrics:
  - metric: "[Supporting metric]"
    target: "[Target value]"
```

### 1.4 User Personas

**Primary Persona:**
```yaml
name: "[Persona name]"
role: "[User role]"
goals:
  - "[What they want to achieve]"
pain_points:
  - "[What frustrates them]"
technical_proficiency: "Beginner | Intermediate | Advanced"
usage_frequency: "Daily | Weekly | Monthly | Occasional"
```

**Secondary Personas:**  
[List other user types who will interact with this feature]

### 1.5 Scope Definition

**✅ In Scope - What WILL be built:**
- [ ] [Specific capability 1]
- [ ] [Specific capability 2]
- [ ] [Specific capability 3]

**❌ Out of Scope - What will NOT be built:**
- [ ] [Explicitly excluded feature]
- [ ] [Future consideration]

**🔮 Future Considerations:**
- [ ] [Potential enhancement for later]

---

## **2. User Experience Specification**

### 2.1 User Journey Map

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Entry     │────▶│   Action    │────▶│   Result    │────▶│    Exit     │
│   Point     │     │   Taken     │     │  Displayed  │     │   Point     │
└─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘
```

**Detailed Flow:**

#### Step 1: [Entry Point Name]
**User Action:** [What the user does]  
**System Response:** [What happens immediately]  
**UI Elements Visible:**
- [Element 1: Button, form, etc.]
- [Element 2: Text, icon, etc.]

**Example:**
```
Step 1: User Opens Scheduling Interface
- User Action: Clicks "Schedule Post" button on post editor
- System Response: Opens scheduling modal overlay
- UI Elements Visible:
  - Date picker (calendar view)
  - Time selector (dropdown)
  - Timezone selector (dropdown with search)
  - "Schedule" button (primary CTA)
  - "Cancel" button (secondary CTA)
```

#### Step 2: [Action Point Name]
[Continue for each step in the user journey]

### 2.2 User Stories

#### Primary User Story
```
As a [user persona]
I want to [action/capability]
So that [benefit/outcome]
```

**Acceptance Criteria:**
```gherkin
Given [initial context/state]
When [action taken]
Then [expected result]
And [additional expected result]

Example:
Given I am logged in as a content creator
And I have composed a post
When I click "Schedule Post"
And I select a date 3 days in the future
And I select a time of 2:00 PM
And I select timezone "America/New_York"
And I click "Confirm Schedule"
Then the post is saved with status "SCHEDULED"
And I see a confirmation message "Post scheduled for Jan 15, 2024 at 2:00 PM EST"
And the post appears in my "Scheduled Posts" list
And I receive an email confirmation
```

#### Secondary User Stories
[List 3-5 additional user stories covering different scenarios]

### 2.3 UI/UX Requirements

#### 2.3.1 Visual Design Specifications

**Layout:**
```yaml
component_type: "Modal | Page | Drawer | Inline | Dropdown"
dimensions:
  width: "[px or % or responsive]"
  height: "[px or % or responsive]"
  max_width: "[px]"
  max_height: "[px]"
position: "Center | Top-right | Full-screen"
responsive_behavior: "[How it adapts to mobile/tablet]"
```

**Color Scheme:**
```yaml
primary_color: "#HEX"
secondary_color: "#HEX"
success_state: "#HEX"
error_state: "#HEX"
warning_state: "#HEX"
disabled_state: "#HEX"
```

**Typography:**
```yaml
heading: "Font family, size, weight"
body_text: "Font family, size, weight"
button_text: "Font family, size, weight"
error_text: "Font family, size, weight"
```

**Spacing:**
```yaml
padding: "[px or rem]"
margin: "[px or rem]"
gap_between_elements: "[px or rem]"
```

#### 2.3.2 Interactive Elements

**Buttons:**

| Button Name | Type | State | Label | Action | Disabled When |
|-------------|------|-------|-------|--------|---------------|
| Schedule | Primary | Enabled | "Schedule Post" | Submits form | Required fields empty |
| Schedule | Primary | Loading | "Scheduling..." | Shows spinner | During API call |
| Schedule | Primary | Success | "Scheduled ✓" | Closes modal | After success (2s) |
| Cancel | Secondary | Enabled | "Cancel" | Closes modal | Never |

**Input Fields:**

| Field Name | Type | Placeholder | Default Value | Validation | Error Message |
|------------|------|-------------|---------------|------------|---------------|
| Date | Date Picker | "Select date" | Tomorrow | Must be future date | "Date must be in the future" |
| Time | Time Picker | "Select time" | Current time + 1hr | Valid 24h format | "Invalid time format" |
| Timezone | Dropdown | "Select timezone" | User's detected TZ | Must be valid IANA timezone | "Invalid timezone" |

**Feedback Elements:**

| Element | Type | Trigger | Message | Duration | Dismissible |
|---------|------|---------|---------|----------|-------------|
| Success Toast | Toast | Successful schedule | "Post scheduled successfully" | 3 seconds | Yes |
| Error Toast | Toast | Failed schedule | "Failed to schedule post. Please try again." | 5 seconds | Yes |
| Loading Spinner | Inline | During save | N/A | Until complete | No |
| Validation Error | Inline | Invalid input | Field-specific message | Until corrected | No |

#### 2.3.3 Accessibility Requirements

```yaml
wcag_level: "AA | AAA"
keyboard_navigation:
  - "Tab through all interactive elements"
  - "Enter/Space to activate buttons"
  - "Escape to close modal"
  - "Arrow keys for date picker navigation"
  
screen_reader:
  - "All images have alt text"
  - "Form labels properly associated"
  - "Error messages announced"
  - "Status changes announced"
  
color_contrast:
  - "Text: minimum 4.5:1 ratio"
  - "Large text: minimum 3:1 ratio"
  - "Interactive elements: minimum 3:1 ratio"
  
focus_indicators:
  - "Visible focus outline on all interactive elements"
  - "Focus order follows logical reading order"
  
aria_labels:
  - button_schedule: "Schedule post for future publication"
  - button_cancel: "Cancel scheduling and return to editor"
  - input_date: "Select publication date"
```

### 2.4 Interaction Patterns

#### 2.4.1 User Input Patterns

**Pattern: Date Selection**
```yaml
interaction_type: "Click to open calendar"
input_method: 
  - "Click on date in calendar"
  - "Type date in format MM/DD/YYYY"
  - "Use arrow keys to navigate"
validation_timing: "On blur and on submit"
feedback_timing: "Immediate for invalid format"
```

**Pattern: Form Submission**
```yaml
trigger: "Click 'Schedule' button OR press Enter"
validation_sequence:
  1. "Client-side validation"
  2. "Show loading state"
  3. "API call"
  4. "Server-side validation"
  5. "Success/error response"
optimistic_ui: false
debounce_delay: "None (single submission)"
```

#### 2.4.2 System Feedback Patterns

**Loading States:**
```yaml
initial_load:
  trigger: "Component mounts"
  indicator: "Skeleton screen"
  duration: "Until data loaded"
  
action_processing:
  trigger: "User submits form"
  indicator: "Button spinner + disabled state"
  duration: "Until API response"
  
background_sync:
  trigger: "Scheduled time reached"
  indicator: "Status badge updates"
  duration: "N/A (automatic)"
```

**Error Recovery:**
```yaml
error_type: "Network failure"
user_action: "Retry automatically (3 attempts)"
fallback: "Show error message with manual retry button"
data_preservation: "Form data saved in local storage"
```

### 2.5 Empty States

**No Scheduled Posts:**
```yaml
illustration: "Calendar icon with clock"
heading: "No scheduled posts yet"
description: "Schedule posts to publish automatically at your chosen time"
cta_button: "Schedule Your First Post"
cta_action: "Opens scheduling modal"
```

**Failed Scheduled Posts:**
```yaml
illustration: "Warning icon"
heading: "Some posts failed to publish"
description: "Review and reschedule the posts that couldn't be published"
cta_button: "View Failed Posts"
cta_action: "Navigates to failed posts list"
```

### 2.6 Loading States

| State | Visual | Duration | User Can |
|-------|--------|----------|----------|
| Initial Load | Skeleton screen | 0-2s | Wait |
| Submitting | Button spinner | 0-5s | Wait (button disabled) |
| Processing | Progress bar | 5-30s | Navigate away (background) |
| Refreshing | Pull-to-refresh | 0-2s | Release to trigger |

---

## **3. Functional Requirements**

### 3.1 Core Functionality

#### Feature Capability 1: [Capability Name]

**Description:**  
[Detailed explanation of what this capability does]

**Functional Flow:**
```
1. User initiates action
   ├─ Input: [What user provides]
   ├─ Validation: [What is checked]
   └─ If valid: proceed to step 2
       If invalid: show error [ERROR_CODE]

2. System processes request
   ├─ Action: [What system does]
   ├─ External calls: [APIs, services called]
   └─ Data transformations: [How data is modified]

3. System returns result
   ├─ Success: [What happens on success]
   └─ Failure: [What happens on failure]

4. User sees outcome
   ├─ UI update: [What changes on screen]
   └─ Notifications: [What messages are shown]
```

**Business Rules:**

**Rule BR-001: Future Date Requirement**
```yaml
rule_id: "BR-001"
description: "Scheduled date must be in the future"
condition: "scheduled_datetime > current_datetime"
action_if_true: "Accept scheduling request"
action_if_false: "Reject with error PAST_DATE_NOT_ALLOWED"
priority: "HIGH"
cannot_be_overridden: true

test_cases:
  - input: { scheduled_datetime: "2024-01-15T14:00:00Z", current_datetime: "2024-01-10T10:00:00Z" }
    expected: "ACCEPT"
  - input: { scheduled_datetime: "2024-01-05T14:00:00Z", current_datetime: "2024-01-10T10:00:00Z" }
    expected: "REJECT - PAST_DATE_NOT_ALLOWED"
  - input: { scheduled_datetime: "2024-01-10T10:00:01Z", current_datetime: "2024-01-10T10:00:00Z" }
    expected: "ACCEPT (1 second in future is valid)"
```

**Rule BR-002: Maximum Scheduling Window**
```yaml
rule_id: "BR-002"
description: "Cannot schedule more than 1 year in advance"
condition: "scheduled_datetime <= current_datetime + 365 days"
action_if_true: "Accept scheduling request"
action_if_false: "Reject with error SCHEDULE_TOO_FAR"
priority: "MEDIUM"
configurable: true
configuration_key: "max_schedule_days_ahead"

test_cases:
  - input: { scheduled_datetime: "2025-01-09T14:00:00Z", current_datetime: "2024-01-10T10:00:00Z" }
    expected: "ACCEPT (364 days ahead)"
  - input: { scheduled_datetime: "2025-01-11T14:00:00Z", current_datetime: "2024-01-10T10:00:00Z" }
    expected: "REJECT - SCHEDULE_TOO_FAR (366 days ahead)"
```

**Rule BR-003: Concurrent Scheduling Limit**
```yaml
rule_id: "BR-003"
description: "Users can have maximum 50 scheduled posts at once"
condition: "user.scheduled_posts_count < 50"
action_if_true: "Accept scheduling request"
action_if_false: "Reject with error MAX_SCHEDULED_POSTS_REACHED"
priority: "HIGH"
varies_by_plan:
  free: 10
  pro: 50
  enterprise: 500

test_cases:
  - input: { user_plan: "pro", current_scheduled_count: 49 }
    expected: "ACCEPT"
  - input: { user_plan: "pro", current_scheduled_count: 50 }
    expected: "REJECT - MAX_SCHEDULED_POSTS_REACHED"
  - input: { user_plan: "enterprise", current_scheduled_count: 50 }
    expected: "ACCEPT (enterprise limit is 500)"
```

### 3.2 Feature Capabilities Matrix

| Capability | Free Tier | Pro Tier | Enterprise Tier | Notes |
|------------|-----------|----------|-----------------|-------|
| Schedule posts | ✅ | ✅ | ✅ | All tiers |
| Max scheduled posts | 10 | 50 | 500 | Per user |
| Timezone support | ✅ | ✅ | ✅ | All timezones |
| Recurring schedules | ❌ | ✅ | ✅ | Pro and above |
| Bulk scheduling | ❌ | ❌ | ✅ | Enterprise only |
| Auto-retry on failure | ❌ | ✅ | ✅ | 3 attempts |
| Priority publishing | ❌ | ❌ | ✅ | Queue jumping |
| Analytics | Basic | Advanced | Custom | Different levels |

### 3.3 User Permissions & Access Control

```yaml
permission_model: "RBAC (Role-Based Access Control)"

roles:
  viewer:
    can:
      - view_scheduled_posts
    cannot:
      - create_scheduled_posts
      - edit_scheduled_posts
      - delete_scheduled_posts
      
  editor:
    inherits: "viewer"
    can:
      - create_scheduled_posts
      - edit_own_scheduled_posts
      - delete_own_scheduled_posts
    cannot:
      - edit_others_scheduled_posts
      - delete_others_scheduled_posts
      
  admin:
    inherits: "editor"
    can:
      - edit_others_scheduled_posts
      - delete_others_scheduled_posts
      - configure_scheduling_settings
      - view_all_scheduled_posts
      
  owner:
    inherits: "admin"
    can:
      - manage_scheduling_permissions
      - export_scheduling_data
```

**Permission Checks:**
```yaml
action: "create_scheduled_post"
checks:
  - authenticated: true
  - has_permission: "create_scheduled_posts"
  - within_plan_limits: true
  - account_active: true
  - not_suspended: true
failure_response:
  - if not authenticated: 401 UNAUTHORIZED
  - if no permission: 403 FORBIDDEN
  - if over limit: 403 PLAN_LIMIT_EXCEEDED
  - if account inactive: 403 ACCOUNT_INACTIVE
  - if suspended: 403 ACCOUNT_SUSPENDED
```

---

## **4. Technical Implementation Specification**

### 4.1 System Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                        Client Layer                           │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐            │
│  │  Web App   │  │ Mobile App │  │   API      │            │
│  │  (React)   │  │  (Native)  │  │  Clients   │            │
│  └─────┬──────┘  └─────┬──────┘  └─────┬──────┘            │
└────────┼───────────────┼───────────────┼────────────────────┘
         │               │               │
         └───────────────┴───────────────┘
                         │
         ┌───────────────▼───────────────┐
         │      API Gateway / Load       │
         │         Balancer              │
         └───────────────┬───────────────┘
                         │
         ┌───────────────▼───────────────┐
         │     Application Layer         │
         │  ┌──────────────────────┐    │
         │  │  Scheduling Service  │    │
         │  └──────────┬───────────┘    │
         │             │                 │
         │  ┌──────────▼───────────┐    │
         │  │   Business Logic     │    │
         │  └──────────┬───────────┘    │
         └─────────────┼─────────────────┘
                       │
         ┌─────────────▼─────────────┐
         │      Data Layer           │
         │  ┌──────────┐ ┌─────────┐│
         │  │PostgreSQL│ │  Redis  ││
         │  │    DB    │ │  Cache  ││
         │  └──────────┘ └─────────┘│
         └───────────────────────────┘
                       │
         ┌─────────────▼─────────────┐
         │   Background Jobs Layer   │
         │  ┌──────────────────────┐ │
         │  │  Job Queue (Bull)    │ │
         │  └──────────┬───────────┘ │
         │             │              │
         │  ┌──────────▼───────────┐ │
         │  │  Scheduler Worker    │ │
         │  │  (Cron/Polling)      │ │
         │  └──────────────────────┘ │
         └───────────────────────────┘
```

### 4.2 Data Models

#### 4.2.1 Database Schema

**Table: `scheduled_posts`**

```sql
CREATE TABLE scheduled_posts (
  -- Primary Key
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  
  -- Foreign Keys
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  post_id UUID REFERENCES posts(id) ON DELETE SET NULL,
  organization_id UUID REFERENCES organizations(id) ON DELETE CASCADE,
  
  -- Scheduling Data
  scheduled_datetime TIMESTAMP WITH TIME ZONE NOT NULL,
  timezone VARCHAR(50) NOT NULL, -- IANA timezone (e.g., 'America/New_York')
  
  -- Post Content (stored until published)
  content_type VARCHAR(20) NOT NULL, -- 'text', 'image', 'video', 'link'
  content_data JSONB NOT NULL, -- Flexible storage for different content types
  
  -- Status Management
  status VARCHAR(20) NOT NULL DEFAULT 'pending',
    -- Values: 'pending', 'processing', 'published', 'failed', 'cancelled'
  
  -- Retry Logic
  retry_count INTEGER NOT NULL DEFAULT 0,
  max_retries INTEGER NOT NULL DEFAULT 3,
  last_retry_at TIMESTAMP WITH TIME ZONE,
  next_retry_at TIMESTAMP WITH TIME ZONE,
  
  -- Error Tracking
  error_code VARCHAR(50),
  error_message TEXT,
  error_details JSONB,
  
  -- Metadata
  created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  published_at TIMESTAMP WITH TIME ZONE,
  cancelled_at TIMESTAMP WITH TIME ZONE,
  cancelled_by UUID REFERENCES users(id),
  
  -- Audit Trail
  created_by UUID NOT NULL REFERENCES users(id),
  updated_by UUID REFERENCES users(id),
  
  -- Constraints
  CONSTRAINT valid_status CHECK (status IN ('pending', 'processing', 'published', 'failed', 'cancelled')),
  CONSTRAINT future_schedule CHECK (scheduled_datetime > created_at),
  CONSTRAINT valid_retry_count CHECK (retry_count >= 0 AND retry_count <= max_retries),
  CONSTRAINT valid_timezone CHECK (timezone ~ '^[A-Za-z]+/[A-Za-z_]+$')
);

-- Indexes for Performance
CREATE INDEX idx_scheduled_posts_user_id ON scheduled_posts(user_id);
CREATE INDEX idx_scheduled_posts_status ON scheduled_posts(status);
CREATE INDEX idx_scheduled_posts_scheduled_datetime ON scheduled_posts(scheduled_datetime);
CREATE INDEX idx_scheduled_posts_next_retry ON scheduled_posts(next_retry_at) WHERE status = 'failed';
CREATE INDEX idx_scheduled_posts_organization ON scheduled_posts(organization_id);

-- Composite Index for Common Query
CREATE INDEX idx_scheduled_posts_user_status_datetime 
  ON scheduled_posts(user_id, status, scheduled_datetime DESC);

-- Partial Index for Active Schedules
CREATE INDEX idx_scheduled_posts_active 
  ON scheduled_posts(scheduled_datetime) 
  WHERE status IN ('pending', 'processing');
```

**Table: `scheduled_post_history`**

```sql
CREATE TABLE scheduled_post_history (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  scheduled_post_id UUID NOT NULL REFERENCES scheduled_posts(id) ON DELETE CASCADE,
  
  -- Event Data
  event_type VARCHAR(50) NOT NULL, 
    -- 'created', 'updated', 'published', 'failed', 'retried', 'cancelled'
  previous_status VARCHAR(20),
  new_status VARCHAR(20),
  
  -- Change Details
  changes JSONB, -- What changed
  triggered_by VARCHAR(20) NOT NULL, -- 'user', 'system', 'cron'
  triggered_by_user_id UUID REFERENCES users(id),
  
  -- Metadata
  created_at TIMESTAMP WITH TIME ZONE NOT NULL DEFAULT NOW(),
  
  -- Constraints
  CONSTRAINT valid_event_type CHECK (event_type IN (
    'created', 'updated', 'published', 'failed', 'retried', 'cancelled', 'rescheduled'
  ))
);

CREATE INDEX idx_scheduled_post_history_post_id ON scheduled_post_history(scheduled_post_id);
CREATE INDEX idx_scheduled_post_history_created_at ON scheduled_post_history(created_at DESC);
```

#### 4.2.2 Data Model Definitions

**Model: ScheduledPost**

```typescript
interface ScheduledPost {
  // Identifiers
  id: string;                    // UUID v4
  user_id: string;               // UUID v4
  post_id: string | null;        // UUID v4 (null until published)
  organization_id: string;       // UUID v4
  
  // Scheduling
  scheduled_datetime: string;    // ISO 8601 with timezone
  timezone: string;              // IANA timezone identifier
  
  // Content
  content_type: ContentType;
  content_data: ContentData;
  
  // Status
  status: ScheduleStatus;
  
  // Retry Logic
  retry_count: number;           // 0-max_retries
  max_retries: number;           // Default: 3
  last_retry_at: string | null;  // ISO 8601
  next_retry_at: string | null;  // ISO 8601
  
  // Error Tracking
  error_code: string | null;
  error_message: string | null;
  error_details: Record<string, any> | null;
  
  // Timestamps
  created_at: string;            // ISO 8601
  updated_at: string;            // ISO 8601
  published_at: string | null;   // ISO 8601
  cancelled_at: string | null;   // ISO 8601
  cancelled_by: string | null;   // UUID v4
  
  // Audit
  created_by: string;            // UUID v4
  updated_by: string | null;     // UUID v4
}

type ScheduleStatus = 
  | 'pending'      // Waiting for scheduled time
  | 'processing'   // Currently being published
  | 'published'    // Successfully published
  | 'failed'       // Failed after all retries
  | 'cancelled';   // Manually cancelled

type ContentType = 
  | 'text'
  | 'image'
  | 'video'
  | 'link'
  | 'poll'
  | 'carousel';

interface ContentData {
  // Common fields
  text?: string;
  
  // Type-specific fields
  media_urls?: string[];
  link_url?: string;
  link_preview?: {
    title: string;
    description: string;
    image_url: string;
  };
  poll_options?: string[];
  poll_duration_hours?: number;
  
  // Metadata
  tags?: string[];
  mentions?: string[];
  location?: {
    name: string;
    latitude: number;
    longitude: number;
  };
}
```

#### 4.2.3 API Request/Response Models

**Request: Create Scheduled Post**

```typescript
interface CreateScheduledPostRequest {
  // Required Fields
  scheduled_datetime: string;    // ISO 8601 with timezone
  timezone: string;              // IANA timezone
  content_type: ContentType;
  content_data: ContentData;
  
  // Optional Fields
  organization_id?: string;      // If posting to organization
  max_retries?: number;          // Override default (1-5)
  
  // Validation Rules
  constraints: {
    scheduled_datetime: {
      format: "ISO 8601 (YYYY-MM-DDTHH:mm:ssZ)",
      must_be_future: true,
      max_days_ahead: 365,
      min_minutes_ahead: 5
    },
    timezone: {
      format: "IANA timezone identifier",
      examples: ["America/New_York", "Europe/London", "Asia/Tokyo"],
      validation: "Must be valid IANA timezone"
    },
    content_data: {
      text: {
        max_length: 5000,
        required_if: "content_type === 'text'"
      },
      media_urls: {
        max_items: 10,
        item_format: "Valid URL",
        required_if: "content_type === 'image' || content_type === 'video'"
      }
    }
  }
}

// Example Valid Request
{
  "scheduled_datetime": "2024-01-15T14:00:00-05:00",
  "timezone": "America/New_York",
  "content_type": "text",
  "content_data": {
    "text": "Hello world! This is a scheduled post.",
    "tags": ["announcement", "scheduled"]
  },
  "max_retries": 3
}
```

**Response: Create Scheduled Post**

```typescript
interface CreateScheduledPostResponse {
  status: "success" | "error";
  data?: {
    scheduled_post: ScheduledPost;
    estimated_publish_time: string;  // ISO 8601
    confirmation_code: string;        // For user reference
  };
  error?: {
    code: string;
    message: string;
    details: Record<string, any>;
  };
  metadata: {
    request_id: string;
    processing_time_ms: number;
    timestamp: string;
  };
}

// Example Success Response
{
  "status": "success",
  "data": {
    "scheduled_post": {
      "id": "550e8400-e29b-41d4-a716-446655440000",
      "user_id": "123e4567-e89b-12d3-a456-426614174000",
      "scheduled_datetime": "2024-01-15T14:00:00-05:00",
      "timezone": "America/New_York",
      "content_type": "text",
      "content_data": {
        "text": "Hello world! This is a scheduled post.",
        "tags": ["announcement", "scheduled"]
      },
      "status": "pending",
      "retry_count": 0,
      "max_retries": 3,
      "created_at": "2024-01-10T10:30:00Z",
      "updated_at": "2024-01-10T10:30:00Z",
      "created_by": "123e4567-e89b-12d3-a456-426614174000"
    },
    "estimated_publish_time": "2024-01-15T19:00:00Z",
    "confirmation_code": "SCH-2024-001234"
  },
  "metadata": {
    "request_id": "req-abc123",
    "processing_time_ms": 145,
    "timestamp": "2024-01-10T10:30:00Z"
  }
}
```

### 4.3 API Endpoints

#### 4.3.1 Endpoint: Create Scheduled Post

```yaml
method: POST
path: /api/v1/scheduled-posts
version: "1.0"
stability: "stable"
rate_limit: "100 requests per hour per user"
authentication: "Required (JWT Bearer token)"
authorization: "Requires 'create_scheduled_posts' permission"
```

**Request Headers:**
```yaml
required:
  Authorization: "Bearer {jwt_token}"
  Content-Type: "application/json"
  X-Request-ID: "UUID v4 (optional, auto-generated if not provided)"
  
optional:
  X-Idempotency-Key: "String (max 255 chars) for idempotent requests"
  X-Organization-ID: "UUID v4 (if posting on behalf of organization)"
```

**Request Body:**
[See CreateScheduledPostRequest above]

**Response Codes:**

| Code | Meaning | When | Response Body |
|------|---------|------|---------------|
| 201 | Created | Successfully scheduled | ScheduledPost object |
| 400 | Bad Request | Invalid input data | Error details |
| 401 | Unauthorized | Missing/invalid auth token | Error message |
| 403 | Forbidden | No permission or plan limit | Error with limit info |
| 409 | Conflict | Duplicate idempotency key | Original scheduled post |
| 422 | Unprocessable Entity | Business rule violation | Error with rule details |
| 429 | Too Many Requests | Rate limit exceeded | Retry-After header |
| 500 | Internal Server Error | Unexpected server error | Generic error |
| 503 | Service Unavailable | Service temporarily down | Retry-After header |

**Error Response Examples:**

```json
// 400 - Validation Error
{
  "status": "error",
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Request validation failed",
    "details": [
      {
        "field": "scheduled_datetime",
        "error": "PAST_DATE_NOT_ALLOWED",
        "message": "Scheduled date must be in the future",
        "received": "2024-01-05T14:00:00Z",
        "current_time": "2024-01-10T10:30:00Z"
      }
    ]
  },
  "metadata": {
    "request_id": "req-abc123",
    "timestamp": "2024-01-10T10:30:00Z"
  }
}

// 403 - Plan Limit Exceeded
{
  "status": "error",
  "error": {
    "code": "PLAN_LIMIT_EXCEEDED",
    "message": "You have reached the maximum number of scheduled posts for your plan",
    "details": {
      "current_count": 10,
      "plan_limit": 10,
      "plan_name": "Free",
      "upgrade_url": "https://example.com/upgrade"
    }
  },
  "metadata": {
    "request_id": "req-abc123",
    "timestamp": "2024-01-10T10:30:00Z"
  }
}

// 422 - Business Rule Violation
{
  "status": "error",
  "error": {
    "code": "SCHEDULE_TOO_FAR",
    "message": "Cannot schedule more than 365 days in advance",
    "details": {
      "rule_id": "BR-002",
      "scheduled_date": "2025-02-01T14:00:00Z",
      "max_allowed_date": "2025-01-10T10:30:00Z",
      "days_ahead": 387,
      "max_days_ahead": 365
    }
  },
  "metadata": {
    "request_id": "req-abc123",
    "timestamp": "2024-01-10T10:30:00Z"
  }
}
```

#### 4.3.2 Endpoint: Get Scheduled Posts

```yaml
method: GET
path: /api/v1/scheduled-posts
version: "1.0"
authentication: "Required"
```

**Query Parameters:**

| Parameter | Type | Required | Default | Valid Values | Description |
|-----------|------|----------|---------|--------------|-------------|
| `status` | string | No | All | `pending`, `processing`, `published`, `failed`, `cancelled` | Filter by status |
| `page` | integer | No | 1 | 1-1000 | Page number |
| `limit` | integer | No | 20 | 1-100 | Items per page |
| `sort` | string | No | `scheduled_datetime` | `scheduled_datetime`, `created_at`, `updated_at` | Sort field |
| `order` | string | No | `asc` | `asc`, `desc` | Sort order |
| `from_date` | string | No | None | ISO 8601 date | Filter from date |
| `to_date` | string | No | None | ISO 8601 date | Filter to date |
| `content_type` | string | No | All | `text`, `image`, `video`, `link` | Filter by content type |

**Example Request:**
```
GET /api/v1/scheduled-posts?status=pending&sort=scheduled_datetime&order=asc&limit=50
```

**Response:**
```json
{
  "status": "success",
  "data": {
    "scheduled_posts": [
      {
        "id": "550e8400-e29b-41d4-a716-446655440000",
        "scheduled_datetime": "2024-01-15T14:00:00-05:00",
        "status": "pending",
        "content_type": "text",
        "content_preview": "Hello world! This is a scheduled...",
        "created_at": "2024-01-10T10:30:00Z"
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 50,
      "total_items": 15,
      "total_pages": 1,
      "has_next": false,
      "has_previous": false
    }
  },
  "metadata": {
    "request_id": "req-xyz789",
    "processing_time_ms": 45,
    "timestamp": "2024-01-10T11:00:00Z"
  }
}
```

#### 4.3.3 Endpoint: Update Scheduled Post

```yaml
method: PATCH
path: /api/v1/scheduled-posts/{id}
version: "1.0"
authentication: "Required"
authorization: "Must own the post or have admin permission"
```

**Path Parameters:**
- `id`: UUID v4 of the scheduled post

**Request Body:**
```json
{
  "scheduled_datetime": "2024-01-16T14:00:00-05:00",
  "timezone": "America/New_York",
  "content_data": {
    "text": "Updated text content"
  }
}
```

**Business Rules:**
- Can only update posts with status `pending`
- Cannot update posts within 5 minutes of scheduled time
- Must re-validate all scheduling rules

**Response:**
```json
{
  "status": "success",
  "data": {
    "scheduled_post": { /* Updated ScheduledPost object */ },
    "changes": {
      "scheduled_datetime": {
        "old": "2024-01-15T14:00:00-05:00",
        "new": "2024-01-16T14:00:00-05:00"
      }
    }
  }
}
```

#### 4.3.4 Endpoint: Cancel Scheduled Post

```yaml
method: DELETE
path: /api/v1/scheduled-posts/{id}
version: "1.0"
authentication: "Required"
authorization: "Must own the post or have admin permission"
```

**Path Parameters:**
- `id`: UUID v4 of the scheduled post

**Query Parameters:**
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `reason` | string | No | Cancellation reason (max 500 chars) |

**Business Rules:**
- Can only cancel posts with status `pending` or `failed`
- Cannot cancel posts with status `processing` or `published`
- Cancellation is permanent (cannot be undone)

**Response:**
```json
{
  "status": "success",
  "data": {
    "scheduled_post_id": "550e8400-e29b-41d4-a716-446655440000",
    "cancelled_at": "2024-01-10T12:00:00Z",
    "cancelled_by": "123e4567-e89b-12d3-a456-426614174000"
  },
  "metadata": {
    "request_id": "req-cancel123",
    "timestamp": "2024-01-10T12:00:00Z"
  }
}
```

**Error Cases:**
```json
// 409 - Cannot Cancel
{
  "status": "error",
  "error": {
    "code": "CANNOT_CANCEL_PROCESSING",
    "message": "Cannot cancel a post that is currently being published",
    "details": {
      "current_status": "processing",
      "cancellable_statuses": ["pending", "failed"]
    }
  }
}
```

---

## **5. Comprehensive Edge Cases**

### 5.1 Scheduling Edge Cases

| Case ID | Scenario | Input Example | Expected Behavior | Error Code | Rationale |
|---------|----------|---------------|-------------------|------------|-----------|
| SCH-001 | Schedule in the past | `scheduled_datetime: "2023-01-01T00:00:00Z"` (current: 2024-01-10) | Reject | `PAST_DATE_NOT_ALLOWED` | Cannot publish in the past |
| SCH-002 | Schedule exactly now | `scheduled_datetime: "2024-01-10T10:30:00Z"` (current: same) | Reject | `MINIMUM_DELAY_REQUIRED` | Need at least 5 min buffer |
| SCH-003 | Schedule 1 second in future | `scheduled_datetime: current + 1 second` | Reject | `MINIMUM_DELAY_REQUIRED` | Too close to current time |
| SCH-004 | Schedule 4 minutes ahead | `scheduled_datetime: current + 4 minutes` | Reject | `MINIMUM_DELAY_REQUIRED` | Below 5-minute minimum |
| SCH-005 | Schedule exactly 5 minutes ahead | `scheduled_datetime: current + 5 minutes` | Accept | - | Meets minimum requirement |
| SCH-006 | Schedule 1 year ahead | `scheduled_datetime: current + 365 days` | Accept | - | Within maximum window |
| SCH-007 | Schedule 366 days ahead | `scheduled_datetime: current + 366 days` | Reject | `SCHEDULE_TOO_FAR` | Exceeds 1-year limit |
| SCH-008 | Schedule on leap day (leap year) | `scheduled_datetime: "2024-02-29T14:00:00Z"` | Accept | - | Valid date in leap year |
| SCH-009 | Schedule on Feb 29 (non-leap) | `scheduled_datetime: "2023-02-29T14:00:00Z"` | Reject | `INVALID_DATE` | Date doesn't exist |
| SCH-010 | Schedule during DST transition (spring) | `scheduled_datetime: "2024-03-10T02:30:00-05:00"` (EST→EDT) | Accept, adjust to 03:30 EDT | - | Handle DST gap |
| SCH-011 | Schedule during DST transition (fall) | `scheduled_datetime: "2024-11-03T01:30:00-04:00"` (EDT→EST) | Accept, use first occurrence | - | Handle DST overlap |
| SCH-012 | Invalid timezone | `timezone: "Invalid/Timezone"` | Reject | `INVALID_TIMEZONE` | Not a valid IANA timezone |
| SCH-013 | Deprecated timezone | `timezone: "US/Eastern"` | Accept, convert to `America/New_York` | - | Handle legacy timezones |
| SCH-014 | UTC timezone | `timezone: "UTC"` | Accept | - | Valid timezone |
| SCH-015 | Timezone with offset | `timezone: "GMT+5"` | Reject | `INVALID_TIMEZONE` | Use IANA format |
| SCH-016 | Mismatched timezone and offset | `scheduled_datetime: "2024-01-15T14:00:00-08:00"`, `timezone: "America/New_York"` | Reject | `TIMEZONE_MISMATCH` | Offset doesn't match timezone |
| SCH-017 | Schedule at midnight | `scheduled_datetime: "2024-01-15T00:00:00Z"` | Accept | - | Valid time |
| SCH-018 | Schedule at 23:59:59 | `scheduled_datetime: "2024-01-15T23:59:59Z"` | Accept | - | Valid time |
| SCH-019 | Schedule with milliseconds | `scheduled_datetime: "2024-01-15T14:00:00.123Z"` | Accept, truncate to seconds | - | Precision to seconds |
| SCH-020 | Schedule with microseconds | `scheduled_datetime: "2024-01-15T14:00:00.123456Z"` | Accept, truncate to seconds | - | Precision to seconds |
| SCH-021 | Duplicate schedule (same time) | Two posts at `"2024-01-15T14:00:00Z"` | Accept both | - | No conflict |
| SCH-022 | Schedule during system maintenance | `scheduled_datetime` during planned downtime | Accept with warning | - | Will retry after maintenance |
| SCH-023 | Schedule on December 31, 23:59 | `scheduled_datetime: "2024-12-31T23:59:00Z"` | Accept | - | Valid end-of-year time |
| SCH-024 | Schedule on January 1, 00:00 | `scheduled_datetime: "2025-01-01T00:00:00Z"` | Accept | - | Valid new year time |
| SCH-025 | Year boundary (365 days from Dec 31) | `scheduled_datetime: "2025-12-31T23:59:00Z"` (current: 2025-01-01) | Accept | - | Exactly 365 days |

### 5.2 Content Validation Edge Cases

| Case ID | Scenario | Input Example | Expected Behavior | Error Code |
|---------|----------|---------------|-------------------|------------|
| CNT-001 | Empty text content | `content_data: { text: "" }` | Reject | `CONTENT_REQUIRED` |
| CNT-002 | Whitespace-only text | `content_data: { text: "   " }` | Reject after trim | `CONTENT_REQUIRED` |
| CNT-003 | Text at max length | `content_data: { text: "x" * 5000 }` | Accept | - |
| CNT-004 | Text exceeds max length | `content_data: { text: "x" * 5001 }` | Reject | `TEXT_TOO_LONG` |
| CNT-005 | Text with emoji | `content_data: { text: "Hello 👋🌍" }` | Accept, count as characters | - |
| CNT-006 | Text with Unicode | `content_data: { text: "Hello 世界" }` | Accept | - |
| CNT-007 | Text with newlines | `content_data: { text: "Line1\nLine2\nLine3" }` | Accept | - |
| CNT-008 | Text with tabs | `content_data: { text: "Col1\tCol2" }` | Accept | - |
| CNT-009 | Text with HTML | `content_data: { text: "<b>Bold</b>" }` | Escape HTML | - |
| CNT-010 | Text with script tags | `content_data: { text: "<script>alert()</script>" }` | Sanitize/reject | `INVALID_CONTENT` |
| CNT-011 | Text with URLs | `content_data: { text: "Check out https://example.com" }` | Accept, auto-link | - |
| CNT-012 | Text with mentions | `content_data: { text: "Hello @username" }` | Accept, validate mentions | - |
| CNT-013 | Text with hashtags | `content_data: { text: "Hello #world" }` | Accept, extract tags | - |
| CNT-014 | Invalid mention | `content_data: { text: "@nonexistentuser" }` | Accept with warning | - |
| CNT-015 | No media URLs (image type) | `content_type: "image"`, `content_data: { media_urls: [] }` | Reject | `MEDIA_REQUIRED` |
| CNT-016 | Single media URL | `content_data: { media_urls: ["https://example.com/img.jpg"] }` | Accept | - |
| CNT-017 | Max media URLs | `content_data: { media_urls: [10 URLs] }` | Accept | - |
| CNT-018 | Exceeds max media | `content_data: { media_urls: [11 URLs] }` | Reject | `TOO_MANY_MEDIA` |
| CNT-019 | Invalid media URL | `content_data: { media_urls: ["not-a-url"] }` | Reject | `INVALID_MEDIA_URL` |
| CNT-020 | Media URL not accessible | `content_data: { media_urls: ["https://example.com/404.jpg"] }` | Accept, validate async | - |
| CNT-021 | Mixed media types | `content_data: { media_urls: ["image.jpg", "video.mp4"] }` | Reject | `MIXED_MEDIA_NOT_ALLOWED` |
| CNT-022 | Duplicate media URLs | `content_data: { media_urls: ["img.jpg", "img.jpg"] }` | Deduplicate | - |
| CNT-023 | Media file too large | URL points to 50MB file (limit: 10MB) | Reject after validation | `MEDIA_TOO_LARGE` |
| CNT-024 | Unsupported media format | `content_data: { media_urls: ["file.exe"] }` | Reject | `UNSUPPORTED_MEDIA_FORMAT` |
| CNT-025 | Link without preview data | `content_type: "link"`, `content_data: { link_url: "https://example.com" }` | Accept, fetch preview async | - |

### 5.3 User Limit Edge Cases

| Case ID | Scenario | User State | Action | Expected Behavior | Error Code |
|---------|----------|------------|--------|-------------------|------------|
| LMT-001 | At limit (Free: 10/10) | Free plan, 10 scheduled posts | Create new | Reject | `PLAN_LIMIT_EXCEEDED` |
| LMT-002 | Below limit (Free: 9/10) | Free plan, 9 scheduled posts | Create new | Accept | - |
| LMT-003 | At limit (Pro: 50/50) | Pro plan, 50 scheduled posts | Create new | Reject | `PLAN_LIMIT_EXCEEDED` |
| LMT-004 | Upgrade from Free to Pro | Free plan, 10 scheduled posts | Upgrade to Pro | Now 10/50, can create more | - |
| LMT-005 | Downgrade from Pro to Free | Pro plan, 25 scheduled posts | Downgrade to Free | Reject downgrade or grandfather existing | `CANNOT_DOWNGRADE` |
| LMT-006 | Cancel post at limit | Free plan, 10/10 scheduled | Cancel one post | Now 9/10, can create new | - |
| LMT-007 | Post publishes at limit | Free plan, 10/10 scheduled | One post publishes | Now 9/10, can create new | - |
| LMT-008 | Concurrent creation at limit | Free plan, 9/10 scheduled | Two simultaneous creates | First succeeds, second rejects | `PLAN_LIMIT_EXCEEDED` |
| LMT-009 | Failed post counts toward limit | Free plan, 10/10 (1 failed) | Create new | Reject (failed counts) | `PLAN_LIMIT_EXCEEDED` |
| LMT-010 | Retry failed post at limit | Free plan, 10/10 (1 failed) | Retry failed post | Accept (doesn't create new) | - |
| LMT-011 | Organization limit | Org has 100 scheduled posts | Member creates new | Check org limit, not user | - |
| LMT-012 | User in multiple orgs | User in 3 orgs | Create in each | Each org has separate limit | - |
| LMT-013 | Expired trial | Trial expired, 5 scheduled posts | Create new | Reject | `TRIAL_EXPIRED` |
| LMT-014 | Suspended account | Account suspended | Create new | Reject | `ACCOUNT_SUSPENDED` |
| LMT-015 | Deleted account | Account soft-deleted | Access scheduled posts | Reject | `ACCOUNT_NOT_FOUND` |

### 5.4 Concurrency & Race Condition Edge Cases

| Case ID | Scenario | Concurrent Actions | Expected Behavior | Implementation |
|---------|----------|-------------------|-------------------|----------------|
| CONC-001 | Duplicate creation | Two identical POST requests | Both succeed with different IDs | No idempotency key |
| CONC-002 | Idempotent creation | Two requests with same idempotency key | First succeeds, second returns same result | Cache idempotency key for 24h |
| CONC-003 | Update during publish | User updates while system publishes | Update rejected | Lock post during publish |
| CONC-004 | Cancel during publish | User cancels while system publishes | Cancel rejected or publish completes | Lock post during publish |
| CONC-005 | Two users update same post | User A and B update simultaneously | Use optimistic locking with version | Include version in WHERE clause |
| CONC-006 | Create at exact limit | Two creates when at 9/10 limit | First succeeds, second rejects | Transaction with row lock |
| CONC-007 | Publish and cancel race | System publishes, user cancels | Publish wins (already processing) | Status transition rules |
| CONC-008 | Double publish attempt | Cron triggers twice for same post | Second attempt skipped | Idempotent publish operation |
| CONC-009 | Update and delete race | User updates and deletes simultaneously | Delete wins | Deletion takes precedence |
| CONC-010 | Retry during manual retry | Auto-retry and manual retry triggered | First retry wins, second skipped | Lock on retry |
| CONC-011 | Multiple workers pick same post | Two workers query for pending posts | Only one processes each post | SELECT FOR UPDATE SKIP LOCKED |
| CONC-012 | Database deadlock | Complex transaction deadlock | Detect and retry | Exponential backoff retry |

### 5.5 Publishing & Retry Edge Cases

| Case ID | Scenario | Situation | Expected Behavior | Retry Strategy |
|---------|----------|-----------|-------------------|----------------|
| PUB-001 | Publish at exact scheduled time | Current time = scheduled time | Publish immediately | - |
| PUB-002 | Publish 1 second late | Current time = scheduled + 1s | Publish immediately | - |
| PUB-003 | Publish 5 minutes late | Current time = scheduled + 5min | Publish with "late" flag | - |
| PUB-004 | Publish 1 hour late (system down) | Current time = scheduled + 1hr | Publish or skip based on config | Configurable: publish or skip |
| PUB-005 | API failure (500 error) | Publishing API returns 500 | Retry 3 times with backoff | Exponential: 1min, 5min, 15min |
| PUB-006 | API timeout | Publishing API times out | Retry 3 times | Same as API failure |
| PUB-007 | Network error | Cannot reach API | Retry 3 times | Same as API failure |
| PUB-008 | Rate limit (429) | Publishing API rate limited | Wait and retry | Respect Retry-After header |
| PUB-009 | Authentication failure (401) | API token expired | Refresh token and retry once | Token refresh + 1 retry |
| PUB-010 | Permanent failure (400) | Invalid content per API | Mark as failed, no retry | No retry for client errors |
| PUB-011 | Content violation | Content violates platform rules | Mark as failed, notify user | No retry |
| PUB-012 | User deleted during schedule | User account deleted | Skip publishing | No retry |
| PUB-013 | Permission revoked | User revoked app permissions | Mark as failed, notify user | No retry |
| PUB-014 | All retries exhausted | Failed 3 times | Mark as permanently failed | No more retries |
| PUB-015 | Manual retry after failure | User manually retries failed post | Reset retry count, attempt again | New retry cycle |
| PUB-016 | Partial publish (multi-platform) | Published to Platform A, failed on B | Mark partial success, retry B only | Platform-specific retry |
| PUB-017 | Database failure during publish | Cannot update status to "published" | Retry entire operation | Transaction rollback + retry |
| PUB-018 | Duplicate publish detection | Post already published | Skip, log warning | Idempotency check |
| PUB-019 | Content changed during retry | User edited content between retries | Publish latest version | Always use latest data |
| PUB-020 | System maintenance during publish | Platform in maintenance mode | Wait and retry after maintenance | Extended retry window |

### 5.6 Timezone & Time Handling Edge Cases

| Case ID | Scenario | Input | Expected Behavior | Notes |
|---------|----------|-------|-------------------|-------|
| TZ-001 | UTC timezone | `timezone: "UTC"`, `scheduled_datetime: "2024-01-15T14:00:00Z"` | Store and publish at exact UTC time | Standard case |
| TZ-002 | Eastern Time (winter) | `timezone: "America/New_York"`, `scheduled_datetime: "2024-01-15T14:00:00-05:00"` | Convert to UTC: 19:00:00Z | EST = UTC-5 |
| TZ-003 | Eastern Time (summer) | `timezone: "America/New_York"`, `scheduled_datetime: "2024-07-15T14:00:00-04:00"` | Convert to UTC: 18:00:00Z | EDT = UTC-4 |
| TZ-004 | DST spring forward (missing hour) | `timezone: "America/New_York"`, `scheduled_datetime: "2024-03-10T02:30:00-05:00"` | Adjust to 03:30:00-04:00 EDT | 2:00-3:00 doesn't exist |
| TZ-005 | DST fall back (duplicate hour) | `timezone: "America/New_York"`, `scheduled_datetime: "2024-11-03T01:30:00-04:00"` | Use first occurrence (EDT) | Ambiguous time |
| TZ-006 | DST fall back (second occurrence) | `timezone: "America/New_York"`, `scheduled_datetime: "2024-11-03T01:30:00-05:00"` | Use second occurrence (EST) | Explicit offset |
| TZ-007 | Timezone without DST | `timezone: "Asia/Tokyo"`, `scheduled_datetime: "2024-01-15T14:00:00+09:00"` | Convert to UTC: 05:00:00Z | Japan has no DST |
| TZ-008 | Half-hour timezone | `timezone: "Asia/Kolkata"`, `scheduled_datetime: "2024-01-15T14:00:00+05:30"` | Convert to UTC: 08:30:00Z | India = UTC+5:30 |
| TZ-009 | 45-minute timezone | `timezone: "Asia/Kathmandu"`, `scheduled_datetime: "2024-01-15T14:00:00+05:45"` | Convert to UTC: 08:15:00Z | Nepal = UTC+5:45 |
| TZ-010 | Negative timezone | `timezone: "America/Los_Angeles"`, `scheduled_datetime: "2024-01-15T14:00:00-08:00"` | Convert to UTC: 22:00:00Z | PST = UTC-8 |
| TZ-011 | Date line crossing | `timezone: "Pacific/Auckland"`, `scheduled_datetime: "2024-01-16T02:00:00+13:00"` | Convert to UTC: 2024-01-15T13:00:00Z | Next day in NZ |
| TZ-012 | Timezone change (historical) | `timezone: "America/New_York"`, `scheduled_datetime: "1970-01-15T14:00:00-05:00"` | Handle historical timezone rules | DST rules changed over time |
| TZ-013 | Future timezone rule change | `timezone: "Europe/Moscow"`, `scheduled_datetime: "2025-01-15T14:00:00+03:00"` | Use current known rules | May need updates |
| TZ-014 | Display in user timezone | User in PST views post scheduled in EST | Show: "Jan 15, 2024 11:00 AM PST" | Convert for display |
| TZ-015 | System timezone vs user timezone | Server in UTC, user in EST | All operations in UTC, display in user TZ | Separation of concerns |

### 5.7 Data Integrity Edge Cases

| Case ID | Scenario | Situation | Expected Behavior | Recovery |
|---------|----------|-----------|-------------------|----------|
| DATA-001 | Database connection lost | Mid-transaction connection drops | Transaction rolled back | Retry entire operation |
| DATA-002 | Partial data save | Some fields saved, others failed | All-or-nothing transaction | Rollback all changes |
| DATA-003 | Foreign key violation | Referenced user deleted | Cascade delete or reject | Depends on FK constraint |
| DATA-004 | Unique constraint violation | Duplicate idempotency key | Return existing record | Idempotent behavior |
| DATA-005 | Data type mismatch | String in integer field | Validation error before DB | Client-side validation |
| DATA-006 | Null in non-nullable field | Required field missing | Validation error | Reject request |
| DATA-007 | JSON field corruption | Invalid JSON in JSONB column | Validation error | Reject request |
| DATA-008 | Character encoding issue | Invalid UTF-8 sequence | Reject or sanitize | Input validation |
| DATA-009 | Database disk full | Cannot write new records | Service unavailable error | Alert ops team |
| DATA-010 | Replication lag | Read replica behind primary | Stale data read | Use primary for critical reads |
| DATA-011 | Index corruption | Query performance degraded | Slower queries, still works | Rebuild index |
| DATA-012 | Backup restoration | Restore from backup | Some recent data lost | Accept data loss window |
| DATA-013 | Data migration in progress | Schema change happening | Maintain backward compatibility | Blue-green deployment |
| DATA-014 | Orphaned records | Post deleted but schedule remains | Cleanup job removes orphans |