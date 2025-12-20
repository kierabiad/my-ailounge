# TODO List - Derived from Jira-tickets-12-18-2025.csv

## High Priority - Immediate Action

*   **MYD-2836: TypeError: 'NoneType' object is not subscriptable (Zoho Integration)**
    *   **Context:** Sentry issue from `sync_session_to_zoho`, indicating a `NoneType` object is being subscripted. This can lead to data loss or incorrect session syncing to Zoho.
    *   **Risk:** High - potential data integrity issues, failed bookings.
    *   **Action:** Investigate `zoho_response['data'][0]['details']['id']` in `zoho/utils/api.py` and ensure `zoho_response` and its keys are handled gracefully, especially when no data is returned.
    *   **Status:** pending
*   **MYD-2832: SwaggerGenerationError (Duplicate Serializer Ref Name)**
    *   **Context:** Sentry issue, duplicate `ref_name` for `WebhookSerializer` in `zoho.webhooks.sessions.main` and `zoho.webhooks.users.main`.
    *   **Risk:** High - API documentation generation failure, potential runtime issues with Swagger.
    *   **Action:** Explicitly set `ref_name` attribute on both serializers' `Meta` classes to be unique.
    *   **Status:** pending
*   **MYD-2819: KeyError: 'user_uuid' (User Creation/OAuth2)**
    *   **Context:** Sentry issue in `users/signals.py` during user creation, related to `oauth2_uuid`.
    *   **Risk:** High - User registration failure, particularly with OAuth2.
    *   **Action:** Ensure `resp['user_uuid']` is always present or handled with a default value during user creation in `create_user` signal.
    *   **Status:** pending
*   **MYD-2699: InvalidHeader: Invalid leading whitespace... (Xendit Integration)**
    *   **Context:** Sentry issue in `payment_gateway/views.py` during `charge_token`, related to Xendit API calls. Invalid header value.
    *   **Risk:** High - Payment processing failures.
    *   **Action:** Inspect header construction for Xendit API calls in `reservations/utils/validators.py` to remove any leading whitespace or invalid characters.
    *   **Status:** pending
*   **MYD-2698: TypeError: string indices must be integers (Xendit Integration)**
    *   **Context:** Sentry issue in `payment_gateway/webhooks/saas.py` during `request_payment_link`.
    *   **Risk:** High - Payment link generation failure, impacting SaaS payments.
    *   **Action:** Investigate `invoice_response['id']` and ensure `invoice_response` is not `None` or an unexpected type.
    *   **Status:** pending
*   **MYD-2688: AttributeError: 'NoneType' object has no attribute 'user' (Zoho User Update)**
    *   **Context:** Sentry issue in `users/views/account.py` and `users/utils/zoho.py` during Zoho user updates.
    *   **Risk:** High - User profile updates failing to sync to Zoho.
    *   **Action:** Ensure `company_email.user` is properly assigned or handled when `company_email` might be `None`.
    *   **Status:** pending
*   **MYD-2648: KeyError: 'email' (Acuity Webhook)**
    *   **Context:** Sentry issue in `mindyou/webhooks/sessions/acuity.py` during Acuity webhook processing.
    *   **Risk:** High - Session data not being processed correctly from Acuity, leading to desyncs.
    *   **Action:** Verify the payload `r_data` from Acuity webhook and ensure the 'email' key is always present or handled.
    *   **Status:** pending
*   **MYD-2612: AttributeError: 'Transaction' object has no attribute 'accounted_datetime' (Refund Workflow)**
    *   **Context:** Sentry issue in `payment_gateway/views.py` and `payment_gateway/utils.py` during refund requests.
    *   **Risk:** High - Refund process failure, incorrect billing.
    *   **Action:** Ensure `transaction.accounted_datetime` exists or provide a default/fallback in `Refund.request_refund` logic.
    *   **Status:** pending
*   **MYD-2600, MYD-2599, MYD-2598, MYD-2597, MYD-2596: Zoho encountered an error / TypeError / AttributeError (Zoho Integration Errors)**
    *   **Context:** A cluster of Sentry issues all related to Zoho API errors, `NoneType` objects, and `capitalize` attribute errors.
    *   **Risk:** High - Widespread Zoho integration failures, data desyncs, and silent errors.
    *   **Action:** Systematically review Zoho API interactions, especially error handling and data parsing. Implement robust checks for `None` values and expected data structures from Zoho responses. Ensure `admin_model.capitalize()` is only called on valid string objects.
    *   **Status:** pending
*   **MYD-2595: AttributeError: 'NoneType' object has no attribute 'has_header' (Django Admin Cache)**
    *   **Context:** Sentry issue related to Django admin cache headers.
    *   **Risk:** High - Potential issues with Django admin functionality and caching.
    *   **Action:** Investigate `patch_response_headers` in `django.utils.cache.py` and ensure `response` object is always valid before checking `has_header`.
    *   **Status:** pending
*   **MYD-2594, MYD-2593, MYD-2537, MYD-2536, MYD-2535, MYD-2534, MYD-2533: JSONDecodeError: Expecting value: line 1 column 1 (char 0) (Acuity/Doctor Availability)**
    *   **Context:** A cluster of Sentry issues all pointing to `JSONDecodeError` when calling Acuity API in `users/tasks/doctors.py` and `users/utils/doctors.py`.
    *   **Risk:** High - Doctor availability and utilization calculations are failing, leading to incorrect booking information and scheduling problems.
    *   **Action:** Review all Acuity API calls, ensure responses are valid JSON, and implement better error handling for non-JSON responses or empty responses. Add logging for raw API responses to aid debugging.
    *   **Status:** pending
*   **MYD-2592: TypeError: list indices must be integers or slices, not str (Zoho Intake Sync)**
    *   **Context:** Sentry issue in `zoho/tasks/sync_intake.py` related to `combined_responses += temp_res['data']`.
    *   **Risk:** High - Intake form data failing to sync to Zoho, data loss.
    *   **Action:** Ensure `temp_res['data']` is always a list or iterable. Implement checks for expected data type before list concatenation.
    *   **Status:** pending
*   **MYD-2581: KeyError: 'Codes' (User Admin CSV Import)**
    *   **Context:** Sentry issue in `users/admin.py` during CSV import, related to deactivating codes.
    *   **Risk:** High - Failure to import user data via CSV, impacting onboarding/offboarding.
    *   **Action:** Verify CSV header and ensure 'Codes' column exists and is correctly parsed during CSV import.
    *   **Status:** pending
*   **MYD-2579: ConnectionError: ('Connection aborted.', ConnectionResetError(104, 'Connection reset by peer')) (Wordpress Integration)**
    *   **Context:** Sentry issue in `resources/services/wordpress.py` when fetching Wordpress content.
    *   **Risk:** High - Resources content failing to load, impacting user experience.
    *   **Action:** Investigate network connectivity and implement retry mechanisms or more robust error handling for external API calls to WordPress.
    *   **Status:** pending
*   **MYD-2578: JSONDecodeError: Expecting value: line 1 column 1 (char 0) (Acuity Admin Grab)**
    *   **Context:** Sentry issue in `mindyou/admin_utils/session.py` when grabbing session data from Acuity.
    *   **Risk:** High - Admin tools failing to fetch Acuity data, impacting support and operational tasks.
    *   **Action:** Similar to other `JSONDecodeError` issues, ensure Acuity API responses are valid JSON.
    *   **Status:** pending
*   **MYD-2543: SystemExit: 1 (Booking Limits)**
    *   **Context:** Sentry issue in `limits/utils.py` related to `_can_user_and_company_book_sessions` and `send_soft_limit_reached.delay`.
    *   **Risk:** High - Booking failures due to unexpected system exit, impacting user experience.
    *   **Action:** Investigate why `SystemExit: 1` is being triggered and ensure `process_session_limits` handles all outcomes gracefully without exiting the application.
    *   **Status:** pending
*   **MYD-2223: TransitionNotAllowed: Can't switch from state 'CANCELLED' using method 'for_payment' (Payment Workflow)**
    *   **Context:** Sentry issue in `payment_gateway/views.py` and `reservations/utils/payment_gateway.py` when creating GCash checkout URL.
    *   **Risk:** High - Payment failures for cancelled sessions that are being re-attempted for payment.
    *   **Action:** Review state transition logic for `session_reservation` to correctly handle `CANCELLED` state when initiating new payment.
    *   **Status:** pending
*   **MYD-1894: Identifier for Cancelled within 24-hours Session status**
    *   **Context:** Need to correctly identify billable cancelled sessions (cancelled by End User within 24 hours) for accurate billing.
    *   **Risk:** High - Incorrect billing, revenue loss, customer dissatisfaction.
    *   **Action:** Implement robust logic to track who initiated the cancellation (End User vs. Admin/Practitioner) and integrate this with the 24-hour cancellation window for billing.
    *   **Status:** pending
*   **MYD-1680: ValueError: Field 'id' expected a number but got 'null' (Session No-Show)**
    *   **Context:** Sentry issue in `mindyou/views/session.py` and `mindyou/utils/main.py` when marking a session as no-show.
    *   **Risk:** High - Failure to correctly mark sessions as no-show, impacting practitioner payments and billing.
    *   **Action:** Ensure `pk` is always a valid integer when fetching `Session.objects.get(pk=pk)`.
    *   **Status:** pending
*   **MYD-1672: TypeError: string indices must be integers (Session Unavailable Dates)**
    *   **Context:** Sentry issue in `mindyou/api/booking.py` and `mindyou/utils/main.py` when generating unavailable dates.
    *   **Risk:** High - Incorrect display of available booking slots, leading to bad user experience.
    *   **Action:** Ensure `d['date']` is always present and correctly formatted as a string.
    *   **Status:** pending
*   **MYD-1671: IntegrityError: duplicate key value violates unique constraint "mindyou_session_appointment_id_cc671318_uniq" (Acuity Webhook)**
    *   **Context:** Sentry issue in `mindyou/webhooks/sessions/acuity.py` during session creation from Acuity webhook.
    *   **Risk:** High - Duplicate session creation from Acuity, leading to data inconsistency.
    *   **Action:** Implement robust check for existing `appointment_id` before creating a new session from Acuity webhook.
    *   **Status:** pending
*   **MYD-1517: [MOBILE]: Missing feature "Saving credit cards"**
    *   **Context:** Critical missing feature for mobile users.
    *   **Risk:** High - Poor user experience, lost conversions for B2C.
    *   **Action:** Prioritize implementation of secure credit card saving functionality for mobile.
    *   **Status:** pending

*   **MYD-1335: TODO: PACKAGE PRICE ADJUST TO [company, practitioner tier, package]**
    *   **Context:** Pricing logic needs refinement.
    *   **Risk:** High - Incorrect billing, revenue leakage.
    *   **Action:** Review and implement robust pricing logic based on company, practitioner tier, and package.
    *   **Status:** pending


## Medium Priority - Technical Debt & Improvements

*   **MYD-3119: [upgrade] [frontend] Bundle from 13 to latest**
    *   **Context:** Frontend framework upgrade.
    *   **Risk:** Medium - Technical debt, potential compatibility issues with older versions.
    *   **Action:** Plan and execute a phased upgrade of the frontend bundle.
    *   **Status:** pending
*   **MYD-3118: [e2e] revamp - booking, scheduling, canceling**
    *   **Context:** Revamp of core E2E flows.
    *   **Risk:** Medium - Complexity, potential regressions if not well-tested.
    *   **Action:** Break down into smaller, manageable tasks with clear acceptance criteria and thorough testing.
    *   **Status:** pending
*   **MYD-3106: [serializers] Look for all unused serializer and remove**
    *   **Context:** Code cleanup and optimization.
    *   **Risk:** Low - Unused code increases bundle size and complexity.
    *   **Action:** Identify and safely remove unused serializers.
    *   **Status:** in_progress
*   **MYD-2980: N+1 Query**
    *   **Context:** Sentry issue, N+1 query in `mood_tracker_usermood`
    *   **Risk:** Medium - Performance degradation, especially under load.
    *   **Action:** Optimize database queries to eliminate N+1 issues.
    *   **Status:** pending
*   **MYD-2979: TypeError: string indices must be integers (Booking API)**
    *   **Context:** Sentry issue in `mindyou/api/booking.py` and `mindyou/utils/session/main.py`.
    *   **Risk:** Medium - Booking API errors.
    *   **Action:** Ensure `d["date"]` is handled correctly.
    *   **Status:** pending
*   **MYD-2978: IntegrityError: null value in column "user_id" (User Terms & Conditions)**
    *   **Context:** Sentry issue in `awesome_portal/views.py` when accepting user terms.
    *   **Risk:** Medium - User onboarding issues.
    *   **Action:** Ensure `user_id` is always present when creating `UserTermsAndConditions` or handle `null` values gracefully.
    *   **Status:** pending
*   **MYD-2977: ValueError: Field 'id' expected a number but got a UUID (Session Sync to Zoho)**
    *   **Context:** Sentry issue in `mindyou/tasks/booking_tasks.py` during `sync_session_to_zoho`.
    *   **Risk:** Medium - Session data not syncing to Zoho.
    *   **Action:** Ensure `session_id` is converted to an integer before querying `Session.objects.get(id=session_id)`.
    *   **Status:** pending
*   **MYD-2976: TemplateDoesNotExist: email/alternate_account_login_attempt.html**
    *   **Context:** Sentry issue in `mindyou/utils/main.py` when sending login attempt emails.
    *   **Risk:** Medium - Users not receiving critical login notifications.
    *   **Action:** Verify the template path and ensure the email template exists.
    *   **Status:** pending
*   **MYD-2975: AttributeError: 'NoneType' object has no attribute 'doctor_detail' (Acuity Webhook)**
    *   **Context:** Sentry issue in `mindyou/webhooks/sessions/acuity.py` when processing Acuity webhooks.
    *   **Risk:** Medium - Acuity webhook processing failures.
    *   **Action:** Ensure `doctor_user.doctor_detail` exists before accessing its attributes.
    *   **Status:** pending
*   **MYD-2974: AttributeError: 'NoneType' object has no attribute 'practitioner_type' (Acuity Webhook)**
    *   **Context:** Sentry issue in `mindyou/webhooks/sessions/acuity.py` when processing Acuity webhooks.
    *   **Risk:** Medium - Acuity webhook processing failures.
    *   **Action:** Ensure `doctor.practitioner_type` exists before accessing it.
    *   **Status:** pending
*   **MYD-2972: "To export company codes, divisions, all fields to Paula Ferrer by Sep 12"**
    *   **Context:** Data export task.
    *   **Risk:** Low - Manual process, potential for errors if not automated.
    *   **Action:** Automate this data export if it's a recurring task.
    *   **Status:** pending
*   **MYD-2964: [api] [contract] remove end date, if no end date, then unlimited**
    *   **Context:** Contract logic improvement.
    *   **Risk:** Low - Manual contract management if not implemented.
    *   **Action:** Modify contract models and logic to handle unlimited end dates.
    *   **Status:** pending
*   **MYD-2963: [saas] double check recurring payment, if they have been charged the same or not**
    *   **Context:** Recurring payment verification.
    *   **Risk:** Medium - Billing discrepancies.
    *   **Action:** Implement a reconciliation process for recurring payments.
    *   **Status:** pending
*   **MYD-2962: [api] restrict dashboard access requests to roles**
    *   **Context:** Security enhancement.
    *   **Risk:** Medium - Unauthorized access if not implemented.
    *   **Action:** Implement role-based access control for dashboard access.
    *   **Status:** pending
*   **MYD-2959: [optimization] next available date (in availabilities)**
    *   **Context:** Performance optimization for availability.
    *   **Risk:** Medium - Slow loading of availability data.
    *   **Action:** Optimize the calculation of the next available date.
    *   **Status:** pending
*   **MYD-2958: Pending records admin → button → mark payout**
    *   **Context:** Part of a larger payout feature.
    *   **Risk:** Low - Manual payouts, potential for delays.
    *   **Action:** Implement the "mark payout" functionality in the admin.
    *   **Status:** staging
*   **MYD-2955: [aws] [devops] [pipelines] add build statistics for deployments and all others (to separate in subtasks)**
    *   **Context:** DevOps improvement.
    *   **Risk:** Low - Lack of visibility into deployment metrics.
    *   **Action:** Implement build statistics tracking in pipelines.
    *   **Status:** pending
*   **MYD-2954: [jira] investigate the integration so we can press story points inside our tickets**
    *   **Context:** Jira integration improvement.
    *   **Risk:** Low - Inefficient story point tracking.
    *   **Action:** Investigate Jira integration capabilities for story points.
    *   **Status:** pending
*   **MYD-2953: [aws] investigate celery -> lambda for cheaper options**
    *   **Context:** Cost optimization.
    *   **Risk:** Low - Higher cloud costs.
    *   **Action:** Research and evaluate migrating Celery tasks to Lambda.
    *   **Status:** pending
*   **MYD-2952: "Hello, seeking some help. There’s no appointment data for today for patient Michelle Balas, EID 102204576. Thank you! - [manual zoho]"**
    *   **Context:** Support request, data discrepancy.
    *   **Risk:** Medium - Customer dissatisfaction, manual intervention required.
    *   **Action:** Investigate why appointment data is missing and if manual Zoho intervention is still needed.
    *   **Status:** pending
*   **MYD-2951: # TODO: need to clean this availability times into a serializer class GetDocAvailabilityTimes**
    *   **Context:** Code cleanup and refactoring.
    *   **Risk:** Low - Untidy code, potential for bugs.
    *   **Action:** Create a dedicated serializer for doctor availability times.
    *   **Status:** pending
*   **MYD-2950: # TODO: this param network for api calls doesnt work**
    *   **Context:** API call issue.
    *   **Risk:** Medium - API calls failing due to incorrect network parameters.
    *   **Action:** Debug and fix the network parameter in API calls.
    *   **Status:** pending
*   **MYD-2949: # TODO: many availabilities so we can handle the m2m table**
    *   **Context:** Database modeling/performance issue.
    *   **Risk:** Medium - Performance degradation with many-to-many relationships for availabilities.
    *   **Action:** Optimize m2m table handling for availabilities.
    *   **Status:** pending
*   **MYD-2947: [b2c] [payouts] record pending payouts**
    *   **Context:** Core feature for B2C payouts.
    *   **Risk:** Medium - Incorrect or delayed payouts.
    *   **Action:** Implement the full payout recording and processing workflow.
    *   **Status:** in_progress
*   **MYD-2940: [zoom contact center] hotline contract to wait for confirmation of funds**
    *   **Context:** External integration.
    *   **Risk:** Low - Dependency on external confirmation.
    *   **Action:** Track confirmation of funds for Zoom contact center contract.
    *   **Status:** pending
*   **MYD-2936: [community] automation for post generation**
    *   **Context:** Community feature enhancement.
    *   **Risk:** Low - Manual content generation.
    *   **Action:** Implement automation for community post generation.
    *   **Status:** pending
*   **MYD-2935: [saas] automate contracts for clients**
    *   **Context:** SaaS operational improvement.
    *   **Risk:** Medium - Manual contract management, potential for errors.
    *   **Action:** Implement automated contract generation for SaaS clients.
    *   **Status:** pending
*   **MYD-2934: [AWS] Cleanup/Removal of Services from Invoice**
    *   **Context:** AWS cost optimization.
    *   **Risk:** Low - Unnecessary AWS costs.
    *   **Action:** Identify and remove unused AWS services.
    *   **Status:** pending
*   **MYD-2922: [deluge] prevent dplicates in emergency contact details subform [crm] [creator]**
    *   **Context:** Data integrity in Zoho CRM.
    *   **Risk:** Medium - Duplicate emergency contact details.
    *   **Action:** Implement deduplication logic for emergency contact details in Zoho.
    *   **Status:** pending
*   **MYD-2910: [email] [google] all file contents are being converted to base64 values when sent via out email**
    *   **Context:** Email attachment issue.
    *   **Risk:** Low - Inefficient email attachments, larger email sizes.
    *   **Action:** Investigate and fix base64 conversion for email attachments.
    *   **Status:** pending
*   **MYD-2902: [zoho] remove all duplicates with regards to emergency contact persons**
    *   **Context:** Data cleanup in Zoho.
    *   **Risk:** Low - Duplicate data in Zoho.
    *   **Action:** Implement a deduplication process for emergency contacts in Zoho.
    *   **Status:** pending
*   **MYD-2899: [dashboard] add mood tracker analytics**
    *   **Context:** New dashboard feature.
    *   **Risk:** Low - Missing analytics for mood tracker.
    *   **Action:** Implement mood tracker analytics in the dashboard.
    *   **Status:** in_progress
*   **MYD-2897: "[api] [admin] all created_by, created_at, updated_by, updated_at should be read_only"**
    *   **Context:** Data integrity and security.
    *   **Risk:** Medium - Accidental modification of audit fields.
    *   **Action:** Enforce read-only status for audit fields in API and admin.
    *   **Status:** pending
*   **MYD-2896: [salesiq] create a dashboard for chatbot analytics**
    *   **Context:** New dashboard feature.
    *   **Risk:** Low - Missing analytics for chatbot.
    *   **Action:** Create a dashboard for SalesIQ chatbot analytics.
    *   **Status:** pending
*   **MYD-2895, MYD-2894, MYD-2892, MYD-2891, MYD-2890: AWS Cost Optimization/Resource Organization**
    *   **Context:** AWS cost and resource management.
    *   **Risk:** Low - Inefficient cloud resource usage, higher costs.
    *   **Action:** Implement AWS Trusted Advisor recommendations, Cost Explorer, and organize resources across accounts.
    *   **Status:** pending
*   **MYD-2877: field to notify developers that sms notification has been sent out**
    *   **Context:** Improved observability.
    *   **Risk:** Low - Lack of visibility into SMS notification status.
    *   **Action:** Implement a notification mechanism for successful SMS sends.
    *   **Status:** pending
*   **MYD-2875: Add API validation for SaaS Emails to prevent spam of emails when erroring out**
    *   **Context:** Prevent email spam from errors.
    *   **Risk:** Medium - Spamming users with error emails.
    *   **Action:** Implement API validation and rate limiting for SaaS emails.
    *   **Status:** pending
*   **MYD-2869: "Fix all workflows for CRM session data - ticked canceled, no show, rescheduled, completed"**
    *   **Context:** CRM workflow fixes.
    *   **Risk:** Medium - Inaccurate CRM data, operational inefficiencies.
    *   **Action:** Review and fix all CRM session data workflows.
    *   **Status:** pending
*   **MYD-2862: KeyError: 'cron_job_sync_session_to_acuity' (Celery Task)**
    *   **Context:** Sentry issue, unregistered Celery task.
    *   **Risk:** Medium - Acuity sync not running, data desync.
    *   **Action:** Ensure the Celery task `cron_job_sync_session_to_acuity` is correctly registered and imported.
    *   **Status:** pending
*   **MYD-2861, MYD-2860: Zoho encountered an error: Status code: 400 (Zoho Integration)**
    *   **Context:** Sentry issues indicating Zoho API errors.
    *   **Risk:** Medium - Zoho integration failures.
    *   **Action:** Investigate the specific Zoho API calls that are failing with 400 errors and address the root cause.
    *   **Status:** staging
*   **MYD-2849: Typescript conversion**
    *   **Context:** Technology migration.
    *   **Risk:** Medium - Large refactoring effort, potential for new bugs.
    *   **Action:** Plan and execute a phased conversion to TypeScript.
    *   **Status:** pending
*   **MYD-2848: [api] affiliate marketing celery automatic exports setup in prod**
    *   **Context:** New feature.
    *   **Risk:** Low - Manual export process if not automated.
    *   **Action:** Implement automated Celery tasks for affiliate marketing exports.
    *   **Status:** pending
*   **MYD-2837: UnboundLocalError: local variable 'company_email' referenced before assignment (Zoho Sync)**
    *   **Context:** Sentry issue in `users/admin.py` during Zoho sync.
    *   **Risk:** Medium - Company email data not syncing to Zoho.
    *   **Action:** Ensure `company_email` is always assigned before being referenced.
    *   **Status:** staging
*   **MYD-2834: "[CRON] add auto send to hans, auto creation of data extraction in photos"**
    *   **Context:** Automation task.
    *   **Risk:** Low - Manual data processing.
    *   **Action:** Implement CRON jobs for data extraction and sending.
    *   **Status:** pending
*   **MYD-2831: "B2B sessions being booked in the portal, but not being booked in Acuity because of "Time is not an available time slot""**
    *   **Context:** B2B booking discrepancy.
    *   **Risk:** Medium - Inconsistent booking data, customer dissatisfaction.
    *   **Action:** Investigate why unavailable time slots are bookable in the portal and fix the sync with Acuity.
    *   **Status:** pending
*   **MYD-2826: [chore] Cleanup debug emails in production to prevent data confusion**
    *   **Context:** Production cleanup.
    *   **Risk:** Low - Debug emails in production.
    *   **Action:** Remove debug email functionality from production.
    *   **Status:** pending
*   **MYD-2822: B2C Acuity and Backend desync**
    *   **Context:** Data desynchronization.
    *   **Risk:** Medium - Inconsistent B2C booking data.
    *   **Action:** Investigate and fix the desync between B2C Acuity and the backend.
    *   **Status:** pending
*   **MYD-2821: [portal] Limit all text inputs (# of characters only) for compliance**
    *   **Context:** Compliance requirement.
    *   **Risk:** Low - Non-compliance if not implemented.
    *   **Action:** Implement character limits for all text inputs in the portal.
    *   **Status:** pending
*   **MYD-2816: [b2b] Add multiple emergency contacts option**
    *   **Context:** Feature enhancement.
    *   **Risk:** Low - Limited emergency contact options.
    *   **Action:** Implement multiple emergency contacts for B2B.
    *   **Status:** pending
*   **MYD-2813: Error when signup in b2c**
    *   **Context:** B2C signup error.
    *   **Risk:** Medium - User onboarding failure.
    *   **Action:** Investigate and fix the B2C signup error.
    *   **Status:** pending
*   **MYD-2796: Fix gender in zoho creator**
    *   **Context:** Data correction in Zoho.
    *   **Risk:** Low - Incorrect gender data in Zoho.
    *   **Action:** Fix gender field mapping and data in Zoho Creator.
    *   **Status:** pending
*   **MYD-2784: #! TODO: * move all base admin actions to this file * move all base fields admin to this file**
    *   **Context:** Code refactoring for Django admin.
    *   **Risk:** Low - Untidy code, maintenance burden.
    *   **Action:** Consolidate base admin actions and fields.
    *   **Status:** pending
*   **MYD-2782: [saas] invoice generation for after payments**
    *   **Context:** SaaS feature.
    *   **Risk:** Low - Manual invoice generation.
    *   **Action:** Implement automated invoice generation for SaaS payments.
    *   **Status:** pending
*   **MYD-2778: "[glow] implementation of created_by should be if dev@my then automatic, if booked by user, should be user, this also should transfer to CRM"**
    *   **Context:** Audit trail improvement.
    *   **Risk:** Low - Incorrect `created_by` attribution.
    *   **Action:** Implement correct `created_by` logic and sync to CRM.
    *   **Status:** pending
*   **MYD-2768: Investigate resources - duplicates**
    *   **Context:** Data quality issue.
    *   **Risk:** Low - Duplicate resources in the system.
    *   **Action:** Investigate and deduplicate resources.
    *   **Status:** pending
*   **MYD-2749: todo: check if all of the models are created since recurring payment would still go through this process**
    *   **Context:** Recurring payment setup.
    *   **Risk:** Medium - Incomplete recurring payment models.
    *   **Action:** Verify all necessary models for recurring payments are created.
    *   **Status:** pending
*   **MYD-2748: "Plan recurring plan for yearly and monthly, to have cancel subscriptions in tact for API calls with Xendit so we can cancel other people's plans"**
    *   **Context:** Recurring payment feature.
    *   **Risk:** Medium - Inability to cancel recurring subscriptions.
    *   **Action:** Plan and implement recurring payment and cancellation logic with Xendit.
    *   **Status:** pending
*   **MYD-2730: captcha / safeguard for saas payment form - to prevent attacks**
    *   **Context:** Security enhancement.
    *   **Risk:** Medium - Bot attacks on payment forms.
    *   **Action:** Implement captcha or other safeguards for SaaS payment forms.
    *   **Status:** pending
*   **MYD-2721: [b2c] [mobile] compiled errors May 2025**
    *   **Context:** Mobile app errors.
    *   **Risk:** Medium - Poor mobile app experience.
    *   **Action:** Investigate and fix compiled errors in the B2C mobile app.
    *   **Status:** pending
*   **MYD-2713: KeyError: 'content' (Wordpress Integration)**
    *   **Context:** Sentry issue in `resources/views/resources.py` and `resources/services/wordpress.py`.
    *   **Risk:** Medium - Wordpress content not loading.
    *   **Action:** Ensure `data['content']` and `data['content']['rendered']` exist in Wordpress API responses.
    *   **Status:** pending
*   **MYD-2639: [aws] create a script that can easily connect the ec2 instances to the target groups**
    *   **Context:** DevOps automation.
    *   **Risk:** Low - Manual EC2 to target group connection.
    *   **Action:** Create an automation script for EC2 to target group connection.
    *   **Status:** pending
*   **MYD-2638: [aws] create a script that can easily spin up an ec2 instance with b2c access for RDS**
    *   **Context:** DevOps automation.
    *   **Risk:** Low - Manual EC2 instance provisioning.
    *   **Action:** Create an automation script to spin up EC2 instances with B2C RDS access.
    *   **Status:** pending
*   **MYD-2633: User Deactivation v2**
    *   **Context:** User management workflow.
    *   **Risk:** Medium - Inefficient user deactivation process.
    *   **Action:** Implement User Deactivation v2 workflow.
    *   **Status:** pending
*   **MYD-2629: """Rogue"" session data in CRM"**
    *   **Context:** Data anomaly in CRM.
    *   **Risk:** Medium - Inaccurate session data in CRM, operational issues.
    *   **Action:** Investigate and clean up "rogue" session data in CRM.
    *   **Status:** pending
*   **MYD-2627: "[api] b2b payment bookings unavailable, stuck in pending payment always"**
    *   **Context:** B2B payment booking issue.
    *   **Risk:** Medium - B2B bookings failing.
    *   **Action:** Investigate and fix B2B payment bookings stuck in pending.
    *   **Status:** pending
*   **MYD-2625: Confirmation of bookings for practitioners**
    *   **Context:** Feature for practitioners.
    *   **Risk:** Low - Lack of confirmation for practitioners.
    *   **Action:** Implement booking confirmation for practitioners.
    *   **Status:** pending
*   **MYD-2624: Cancellations from psychologists should not show up in cancellation count**
    *   **Context:** Analytics accuracy.
    *   **Risk:** Low - Inaccurate cancellation metrics.
    *   **Action:** Adjust cancellation count logic to exclude psychologist cancellations.
    *   **Status:** pending
*   **MYD-2609: B2C Acuity New Appointment Scheduled Webhook Disabled**
    *   **Context:** Acuity webhook issue.
    *   **Risk:** Medium - B2C bookings not syncing from Acuity.
    *   **Action:** Re-enable and verify the B2C Acuity "New Appointment Scheduled" webhook.
    *   **Status:** pending
*   **MYD-2607: Change helpline access for certain b2b companies**
    *   **Context:** Access control.
    *   **Risk:** Low - Incorrect helpline access for B2B companies.
    *   **Action:** Implement logic to manage helpline access based on B2B companies.
    *   **Status:** pending
*   **MYD-2545: Add a layer for checking practitioner type validity inside bookings and reschedules**
    *   **Context:** Booking validation.
    *   **Risk:** Medium - Invalid practitioner types in bookings.
    *   **Action:** Add validation for practitioner types during booking and rescheduling.
    *   **Status:** pending
*   **MYD-2523: [Mood tracker] show this in the reports dashboard**
    *   **Context:** Reporting feature.
    *   **Risk:** Low - Missing mood tracker data in reports.
    *   **Action:** Display mood tracker data in the reports dashboard.
    *   **Status:** pending
*   **MYD-2513: Endpoint Regression**
    *   **Context:** Sentry issue, regression on `/v1/api/resources/podcast-episodes/` duration.
    *   **Risk:** Medium - Incorrect podcast episode data.
    *   **Action:** Investigate and fix the regression in the podcast episodes endpoint.
    *   **Status:** pending
*   **MYD-2460: Finish all pending google console updates to prevent the app from being taken down**
    *   **Context:** App store compliance.
    *   **Risk:** High - App being removed from Google Play Store.
    *   **Action:** Prioritize and complete all pending Google Console updates.
    *   **Status:** pending
*   **MYD-2459: Review and polish Zoho integration in assessments**
    *   **Context:** Zoho integration improvement.
    *   **Risk:** Low - Suboptimal Zoho integration for assessments.
    *   **Action:** Review and polish Zoho integration for assessments.
    *   **Status:** pending
*   **MYD-2444: Zoho API Limits Optimization**
    *   **Context:** Zoho API usage and cost optimization.
    *   **Risk:** Medium - Hitting Zoho API limits, service disruptions.
    *   **Action:** Implement Celery tasks for Zoho calls, queueing, and concurrent counting to manage API limits. Add logging for Acuity and Zoho failures.
    *   **Status:** pending
*   **MYD-2438: Developer verification for Google Play**
    *   **Context:** App store compliance.
    *   **Risk:** Low - Delay in app updates.
    *   **Action:** Complete developer verification for Google Play.
    *   **Status:** pending
*   **MYD-2436: Couldn't manually update the Zoho link/ID of a company in the backend**
    *   **Context:** Admin functionality issue.
    *   **Risk:** Medium - Inability to correct Zoho links manually, data inconsistency.
    *   **Action:** Investigate and fix the manual update process for Zoho links in the backend.
    *   **Status:** pending
*   **MYD-2400: [hotline] Session data of user should be seen from MHR**
    *   **Context:** Feature for MHR.
    *   **Risk:** Low - MHR unable to see session data.
    *   **Action:** Implement functionality for MHR to view user session data.
    *   **Status:** pending
*   **MYD-2389: improve assessment list pictures**
    *   **Context:** UI/UX improvement.
    *   **Risk:** Low - Suboptimal appearance of assessment list.
    *   **Action:** Improve the pictures in the assessment list.
    *   **Status:** pending
*   **MYD-2373: [api] Acuity Scheduling error - investigate**
    *   **Context:** Acuity scheduling error.
    *   **Risk:** Medium - Double booking instances.
    *   **Action:** Investigate Acuity scheduling errors, particularly double bookings.
    *   **Status:** pending
*   **MYD-2355: [gcash] [accreditation] issues validation file requirements**
    *   **Context:** Payment gateway accreditation.
    *   **Risk:** Medium - GCash integration issues.
    *   **Action:** Address validation file requirements for GCash accreditation.
    *   **Status:** pending
*   **MYD-2349: "create a report for the MBT - user results, user answers, timeframe"**
    *   **Context:** Reporting feature.
    *   **Risk:** Low - Missing reports for MBT.
    *   **Action:** Create a report for MBT user results, answers, and timeframe.
    *   **Status:** pending
*   **MYD-2348: Assessment Switch to Zoho Forms**
    *   **Context:** Technology migration.
    *   **Risk:** Medium - Disruption to assessment process.
    *   **Action:** Plan and execute migration of assessments to Zoho Forms.
    *   **Status:** pending
*   **MYD-2339: Implement Major fixes for the story - User cannot log in -> tries to reset pw -> uses correct pw but cannot log in**
    *   **Context:** Login/password reset issue.
    *   **Risk:** Medium - Users unable to access their accounts.
    *   **Action:** Investigate and fix the login/password reset flow.
    *   **Status:** pending
*   **MYD-2336: [idea] Companies should be able to upload the list by themselves**
    *   **Context:** Operational efficiency feature.
    *   **Risk:** Low - Manual employee management for companies.
    *   **Action:** Develop a portal for companies to manage their users.
    *   **Status:** pending
*   **MYD-2333: Add maximum settings for dependents**
    *   **Context:** Feature enhancement.
    *   **Risk:** Low - Unlimited dependents, potential for abuse.
    *   **Action:** Implement maximum settings for dependents.
    *   **Status:** pending
*   **MYD-2330: AttributeError: 'AcuityLog' object has no attribute 'capitalize' (Slack Notification)**
    *   **Context:** Sentry issue, Slack notification error.
    *   **Risk:** Low - Missing error notifications in Slack.
    *   **Action:** Ensure `admin_model.capitalize()` is only called on valid string objects in Slack notification logic.
    *   **Status:** pending
*   **MYD-2321: User should be able to reset password**
    *   **Context:** Core functionality bug.
    *   **Risk:** Medium - Users unable to reset passwords.
    *   **Action:** Investigate and fix password reset functionality.
    *   **Status:** pending
*   **MYD-2320: Give admin user access for company email having the complete error and response**
    *   **Context:** Admin tool improvement.
    *   **Risk:** Low - Lack of visibility for admins into email errors.
    *   **Action:** Provide admin access to detailed company email errors and responses.
    *   **Status:** pending
*   **MYD-2319: Give admin user access to be able to check if booking is available for a certain user**
    *   **Context:** Admin tool improvement.
    *   **Risk:** Low - Admins unable to check booking availability for users.
    *   **Action:** Provide admin access to check booking availability for users.
    *   **Status:** pending
*   **MYD-2317: Crucial Test Cases | Error Prevention**
    *   **Context:** Quality assurance initiative.
    *   **Risk:** Medium - Insufficient test coverage, future bugs.
    *   **Action:** Identify and implement crucial test cases for error prevention.
    *   **Status:** pending
*   **MYD-2289: AttributeError: module 'collections' has no attribute 'Iterable' (Wordpress Sync)**
    *   **Context:** Sentry issue in `resources/admin.py` and `resources/utils/sync.py` related to Wordpress sync.
    *   **Risk:** Medium - Wordpress content not syncing.
    *   **Action:** Update `collections.Iterable` to `collections.abc.Iterable` or equivalent for Python 3.8+.
    *   **Status:** pending
*   **MYD-2281: IntegrityError: duplicate key value violates unique constraint "users_companyemail_email_key" (Company Email Creation)**
    *   **Context:** Sentry issue in `users/views/main.py` during company email creation.
    *   **Risk:** Medium - Duplicate company emails, data inconsistency.
    *   **Action:** Implement a check for existing company emails before creation or handle the `IntegrityError` gracefully.
    *   **Status:** pending
*   **MYD-2280: ValidationError: ['“Invalid date” value has an invalid date format. It must be in YYYY-MM-DD format.'] (Mood Tracker)**
    *   **Context:** Sentry issue in `mood_tracker/views.py` when posting mood data.
    *   **Risk:** Medium - Mood tracker data not saving correctly.
    *   **Action:** Ensure `mood_date` is in `YYYY-MM-DD` format before saving.
    *   **Status:** pending
*   **MYD-2270: ValidationError: ['“null” value has an invalid date format. It must be in YYYY-MM-DD format.'] (Mood Tracker)**
    *   **Context:** Sentry issue in `mood_tracker/views.py` when fetching more journal entries.
    *   **Risk:** Medium - Mood tracker data retrieval issues.
    *   **Action:** Ensure date values are not `null` or handle `null` gracefully when querying for journal entries.
    *   **Status:** pending
*   **MYD-2262: TypeError: 'NoneType' object is not subscriptable (Zoho End User Sync)**
    *   **Context:** Sentry issue in `users/views/main.py` during Zoho end user sync.
    *   **Risk:** Medium - Zoho end user data not syncing.
    *   **Action:** Ensure `zoho_end_user_response` and its keys are handled gracefully.
    *   **Status:** pending
*   **MYD-2259: FileNotFoundError: [Errno 2] No such file or directory: '/tmp/tmp83zizw12' (CSV Import)**
    *   **Context:** Sentry issue during CSV import in Django admin.
    *   **Risk:** Medium - CSV import failures.
    *   **Action:** Investigate temporary file handling during CSV import and ensure the file exists at the expected path.
    *   **Status:** pending
*   **MYD-2255: User data is being stored in the localstorage**
    *   **Context:** Security concern.
    *   **Risk:** Medium - Sensitive user data exposed in local storage.
    *   **Action:** Implement a secure way to store user data (e.g., HTTP-only cookies, server-side sessions, or in-memory state with appropriate protections).
    *   **Status:** pending
*   **MYD-2248: Introduce Zoho Logs readable error messages to support**
    *   **Context:** Improve support tools.
    *   **Risk:** Low - Support team unable to diagnose Zoho errors effectively.
    *   **Action:** Enhance Zoho logs with human-readable error messages.
    *   **Status:** pending
*   **MYD-2247: Introduce Acuity Logs readable error messages to support to organize tickets**
    *   **Context:** Improve support tools.
    *   **Risk:** Low - Support team unable to diagnose Acuity errors effectively.
    *   **Action:** Enhance Acuity logs with human-readable error messages.
    *   **Status:** pending
*   **MYD-2246: Introduce SMSLogs to support**
    *   **Context:** Improve support tools.
    *   **Risk:** Low - Support team unable to track SMS issues effectively.
    *   **Action:** Introduce SMS logging for support.
    *   **Status:** pending
*   **MYD-2227: todo: booking_eligible is irrelevant and should be removed in the future**
    *   **Context:** Code cleanup.
    *   **Risk:** Low - Unused code.
    *   **Action:** Deprecate and remove `booking_eligible`.
    *   **Status:** pending
*   **MYD-2226: Adjust booking approvals to look at the valid approvals instead of the latest ones**
    *   **Context:** Booking logic improvement.
    *   **Risk:** Low - Incorrect booking approvals.
    *   **Action:** Modify booking approval logic to consider all valid approvals.
    *   **Status:** pending
*   **MYD-2224: Clean PHQ9 Logic**
    *   **Context:** Code quality.
    *   **Risk:** Low - Complex or buggy PHQ9 logic.
    *   **Action:** Refactor and clean up PHQ9 logic.
    *   **Status:** pending
*   **MYD-2218: Adjust OTP error message to frontend**
    *   **Context:** User experience improvement.
    *   **Risk:** Low - Unclear OTP error messages for users.
    *   **Action:** Provide clearer OTP error messages to the frontend.
    *   **Status:** pending
*   **MYD-2210: "[backend api] When adding a company, if zoho account does not exists, it throws 500"**
    *   **Context:** Error handling improvement.
    *   **Risk:** Medium - Server errors when Zoho account is missing.
    *   **Action:** Implement graceful error handling when a Zoho account does not exist during company addition.
    *   **Status:** pending
*   **MYD-2193: Add context for booking cooldowns for the end user so booking will not run complex logics**
    *   **Context:** User experience and performance.
    *   **Risk:** Low - Unclear booking cooldowns for users.
    *   **Action:** Provide clear context for booking cooldowns to users.
    *   **Status:** pending
*   **MYD-2192: Improve the slack notification cooldown so #error-notification will not get spammed**
    *   **Context:** Observability improvement.
    *   **Risk:** Low - Spamming error notifications in Slack.
    *   **Action:** Implement cooldowns for Slack error notifications.
    *   **Status:** pending
*   **MYD-2188: KeyError: 'assessment' (Assessment API)**
    *   **Context:** Sentry issue in `assessments/views.py` and `assessments/serializers.py`.
    *   **Risk:** Medium - Assessment data not loading.
    *   **Action:** Ensure 'assessment' is always present in the context for assessment serializers.
    *   **Status:** staging
*   **MYD-2184: TypeError: argument of type 'NoneType' is not iterable (Zoho Company Sync)**
    *   **Context:** Sentry issue in `users/admin.py` and `users/utils/zoho.py` during Zoho company sync.
    *   **Risk:** Medium - Company data not syncing to Zoho.
    *   **Action:** Ensure `zoho_response` is not `None` before checking for 'code' in `_validate_search_response`.
    *   **Status:** pending
*   **MYD-2182: Hotline responders fill up a private note - the psych will read this private note during the session so he/she can understand this more**
    *   **Context:** Feature for practitioners.
    *   **Risk:** Low - Lack of context for practitioners during sessions.
    *   **Action:** Implement private notes for hotline responders that are visible to practitioners.
    *   **Status:** pending
*   **MYD-2179: MHR notes should be shared with the practitioner for review prior to sessions.**
    *   **Context:** Feature for practitioners.
    *   **Risk:** Low - Lack of context for practitioners during sessions.
    *   **Action:** Implement sharing of MHR notes with practitioners prior to sessions.
    *   **Status:** pending
*   **MYD-2168: "Automatically send request approval on behalf of the user, psychologist would have to fill out a recommendation form"**
    *   **Context:** Workflow automation.
    *   **Risk:** Medium - Manual approval process.
    *   **Action:** Automate request approval and recommendation form for psychologists.
    *   **Status:** pending
*   **MYD-2162: Remove deprecated packages: // Remove these lines django-rest-auth==0.9.5 django-rest-swagger==2.2.0**
    *   **Context:** Technical debt cleanup.
    *   **Risk:** Medium - Using outdated, potentially insecure packages.
    *   **Action:** Remove deprecated packages and replace with modern alternatives.
    *   **Status:** pending
*   **MYD-2154: Cloudflare and cloudfront for the frontend to prevent bots attacks**
    *   **Context:** Security and performance.
    *   **Risk:** Medium - Vulnerability to bot attacks, suboptimal performance.
    *   **Action:** Implement Cloudflare and CloudFront for frontend protection and performance.
    *   **Status:** pending
*   **MYD-2153: "[booking] if user tries to book more than 3 times, block the request in the back for 5 minutes"**
    *   **Context:** Abuse prevention.
    *   **Risk:** Medium - Booking abuse.
    *   **Action:** Implement rate limiting for booking attempts.
    *   **Status:** pending
*   **MYD-2152: Registration leads to captchas to prevent bots from brute inputs**
    *   **Context:** Security.
    *   **Risk:** Medium - Bot registrations.
    *   **Action:** Implement captcha for user registration.
    *   **Status:** pending
*   **MYD-2131: [zoho] Reports Analytics Dashboard update for Hotline Logs binary feedback**
    *   **Context:** Reporting feature.
    *   **Risk:** Low - Missing analytics for hotline logs.
    *   **Action:** Update Zoho Reports Analytics Dashboard for hotline logs feedback.
    *   **Status:** in_progress
*   **MYD-2127: "[hotline] user should not put extra fields in the hotline form, link in desc"**
    *   **Context:** Data integrity for hotline form.
    *   **Risk:** Low - Inconsistent data from hotline form.
    *   **Action:** Restrict extra fields in the hotline form.
    *   **Status:** pending
*   **MYD-2106: Cleanup jumpstart folder and seeds/fixtures**
    *   **Context:** Codebase cleanup.
    *   **Risk:** Low - Unnecessary files, increased repository size.
    *   **Action:** Remove unused jumpstart folder and seeds/fixtures.
    *   **Status:** pending
*   **MYD-2105: Cleanup migrations folder**
    *   **Context:** Codebase cleanup.
    *   **Risk:** Low - Large migrations folder, slower migrations.
    *   **Action:** Clean up old migrations.
    *   **Status:** pending
*   **MYD-2100: TODO fix and standardize calling**
    *   **Context:** Code quality.
    *   **Risk:** Low - Inconsistent API calling conventions.
    *   **Action:** Standardize API calling conventions.
    *   **Status:** pending
*   **MYD-2093: [B2C] Investigate Sep 10 Acuity Booking Issue**
    *   **Context:** Acuity booking issue.
    *   **Risk:** Medium - B2C booking failures.
    *   **Action:** Investigate the specific Acuity booking issue.
    *   **Status:** pending
*   **MYD-2082: create a lambda function to autoscale (downtimes) ec2 instances servers**
    *   **Context:** DevOps automation and cost optimization.
    *   **Risk:** Medium - Manual scaling, potential for downtime/overspending.
    *   **Action:** Create a Lambda function for EC2 autoscaling.
    *   **Status:** pending
*   **MYD-2064: [idea] Connect limits to zoho field so it can automatically trigger zoho's notifications instead of relying in the backend**
    *   **Context:** Zoho integration improvement.
    *   **Risk:** Low - Backend-dependent notifications.
    *   **Action:** Investigate connecting limits to Zoho fields for automated notifications.
    *   **Status:** pending
*   **MYD-2054: Display BPP one action query setup to get numbers easily**
    *   **Context:** Reporting feature.
    *   **Risk:** Low - Difficulty in getting BPP numbers.
    *   **Action:** Implement a one-action query for BPP numbers.
    *   **Status:** pending
*   **MYD-1994: TransitionNotAllowed: Can't switch from state 'COMPLETED' using method 'for_payment' (Payment Workflow)**
    *   **Context:** Sentry issue, payment workflow error.
    *   **Risk:** Medium - Inability to re-process payments for completed transactions.
    *   **Action:** Review state transition logic for payments to allow `for_payment` from `COMPLETED` if necessary, or ensure `for_payment` is not called on completed transactions.
    *   **Status:** pending
*   **MYD-1991: [api] [sheets]Language and Specializations are not syncing properly in bios**
    *   **Context:** Data sync issue.
    *   **Risk:** Low - Inaccurate practitioner bios.
    *   **Action:** Investigate and fix language and specialization sync to bios.
    *   **Status:** pending
*   **MYD-1963: [gsheets] Sync Practitioner Bios Description Richtext Implementation**
    *   **Context:** Data sync issue.
    *   **Risk:** Low - Plain text bios instead of rich text.
    *   **Action:** Implement rich text syncing for practitioner bios from Google Sheets.
    *   **Status:** pending
*   **MYD-1912: Automate Utilization Reports**
    *   **Context:** Reporting automation.
    *   **Risk:** Medium - Manual report generation, delays.
    *   **Action:** Automate generation of utilization reports.
    *   **Status:** pending
*   **MYD-1892: # todo: add validation for response**
    *   **Context:** Code quality.
    *   **Risk:** Low - Unvalidated API responses, potential for unexpected behavior.
    *   **Action:** Add validation for API responses.
    *   **Status:** pending
*   **MYD-1891: Refactor ZohoAPI codes**
    *   **Context:** Code refactoring.
    *   **Risk:** Low - Untidy Zoho API code, maintenance burden.
    *   **Action:** Refactor Zoho API code for better organization and readability.
    *   **Status:** pending
*   **MYD-1877: Duplicate relationship between transaction and session**
    *   **Context:** Database schema issue.
    *   **Risk:** Medium - Data inconsistency, potential for bugs.
    *   **Action:** Investigate and resolve duplicate relationship between transaction and session.
    *   **Status:** pending
*   **MYD-1865: Storybook implementation**
    *   **Context:** Frontend development tool.
    *   **Risk:** Low - Inefficient UI development.
    *   **Action:** Implement Storybook for UI component development.
    *   **Status:** pending
*   **MYD-1860: Deactivation and Deletion of Account**
    *   **Context:** User management workflow.
    *   **Risk:** Medium - Inefficient or incomplete account deactivation/deletion.
    *   **Action:** Implement a comprehensive account deactivation and deletion workflow.
    *   **Status:** pending
*   **MYD-1852: Major Issues with google sign in for staging and prod setup**
    *   **Context:** Authentication issue.
    *   **Risk:** Medium - Google sign-in failures, impacting user onboarding.
    *   **Action:** Investigate and fix Google sign-in issues for staging and production.
    *   **Status:** pending
*   **MYD-1826: Push Notifications App**
    *   **Context:** New feature.
    *   **Risk:** Low - Missing push notification functionality.
    *   **Action:** Develop and implement a push notifications app.
    *   **Status:** pending
*   **MYD-1820: Notify in error-notification slack channel if admin access token expired for oauth2**
    *   **Context:** Observability.
    *   **Risk:** Low - Unaware of expired OAuth2 admin access tokens.
    *   **Action:** Implement Slack notifications for expired OAuth2 admin access tokens.
    *   **Status:** pending
*   **MYD-1819: Topics to cover for new patients (users)**
    *   **Context:** Content/onboarding.
    *   **Risk:** Low - Inconsistent information for new patients.
    *   **Action:** Define and ensure consistent topics for new patients.
    *   **Status:** pending
*   **MYD-1812: Login Attempts and Booking Attempts Log**
    *   **Context:** Security and auditing.
    *   **Risk:** Medium - Lack of visibility into login/booking attempts, potential for abuse.
    *   **Action:** Implement logging for login and booking attempts.
    *   **Status:** pending
*   **MYD-1811: # TODO: deprecate me and use get_valid_transactions_v2**
    *   **Context:** Code cleanup.
    *   **Risk:** Low - Using deprecated code.
    *   **Action:** Replace deprecated transaction retrieval with `get_valid_transactions_v2`.
    *   **Status:** pending
*   **MYD-1792: Create CRON for b2c and b2b prod fixtures from recent updates**
    *   **Context:** DevOps automation.
    *   **Risk:** Low - Stale fixtures, slower development.
    *   **Action:** Create CRON jobs to generate B2C and B2B prod fixtures.
    *   **Status:** pending
*   **MYD-1789: Booking more than 1 at a time**
    *   **Context:** Bug/feature.
    *   **Risk:** Medium - Users able to book multiple sessions unintentionally.
    *   **Action:** Prevent users from booking more than one session at a time if unintended.
    *   **Status:** pending
*   **MYD-1765: # FIXME: this a hack for now because querying distinct id's also need to add the id order in the order_by # which will defeat the purpose of the fixed_order**
    *   **Context:** Code quality, database querying.
    *   **Risk:** Medium - Inefficient or incorrect database queries.
    *   **Action:** Refactor the query to correctly handle distinct IDs and ordering without hacks.
    *   **Status:** pending
*   **MYD-1748: Mobile App Social Media Login Google**
    *   **Context:** Authentication feature.
    *   **Risk:** Medium - Incomplete social media login.
    *   **Action:** Implement Google social media login for mobile app.
    *   **Status:** blocked (by MYD-1715)
*   **MYD-1747: Mobile App Social Media Login**
    *   **Context:** Authentication feature.
    *   **Risk:** Medium - Incomplete social media login.
    *   **Action:** Implement social media logins for mobile app.
    *   **Status:** pending
*   **MYD-1734: Update oauth2 repository readme for setup instruction**
    *   **Context:** Documentation.
    *   **Risk:** Low - Outdated setup instructions.
    *   **Action:** Update OAuth2 repository README with setup instructions.
    *   **Status:** pending
*   **MYD-1717: NLE/NLS Flow Implementation**
    *   **Context:** Core user/company lifecycle management.
    *   **Risk:** High - Inconsistent user/company status, incorrect access, billing issues.
    *   **Action:** Implement the "No Longer Employed" (NLE) and "No Longer Subscribed" (NLS) flows, including CRM integration, notifications, and access control. This is a complex Epic.
    *   **Status:** pending
*   **MYD-1715: Social Media Logins**
    *   **Context:** Authentication feature.
    *   **Risk:** Medium - Limited login options.
    *   **Action:** Implement social media logins.
    *   **Status:** in_progress
*   **MYD-1690: "Linkable everything - like community, journal, booking"**
    *   **Context:** UI/UX improvement.
    *   **Risk:** Low - Disconnected user experience.
    *   **Action:** Make all major features linkable.
    *   **Status:** pending
*   **MYD-1668: N+1 Query (Department)**
    *   **Context:** Sentry issue, N+1 query on `users_department`.
    *   **Risk:** Medium - Performance degradation.
    *   **Action:** Optimize database queries to eliminate N+1 issues in department retrieval.
    *   **Status:** pending
*   **MYD-1666: N+1 Queries Fix (Assessments)**
    *   **Context:** Sentry issue, N+1 query on `mindyou_answerselection`.
    *   **Risk:** Medium - Performance degradation in assessments.
    *   **Action:** Optimize database queries to eliminate N+1 issues in assessment answer selection.
    *   **Status:** pending
*   **MYD-1663: "Add reference to payout, if failed, place output in `reference` field"**
    *   **Context:** Payout error handling.
    *   **Risk:** Low - Missing reference for failed payouts.
    *   **Action:** Add a reference field for failed payout outputs.
    *   **Status:** pending
*   **MYD-1647: Contract settings**
    *   **Context:** Contract management.
    *   **Risk:** Low - Manual contract management.
    *   **Action:** Implement contract settings (start date, end date, session limits).
    *   **Status:** pending
*   **MYD-1645: [api] [zoho] Sync Company Settings - add and sync fields**
    *   **Context:** Zoho integration.
    *   **Risk:** Medium - Inconsistent company settings between backend and Zoho.
    *   **Action:** Add and sync company settings fields to Zoho.
    *   **Status:** pending
*   **MYD-1644: Add company/account triggers adding of `User Company` in backend API**
    *   **Context:** User management.
    *   **Risk:** Low - Manual creation of User Company.
    *   **Action:** Implement triggers to automatically add `User Company`.
    *   **Status:** pending
*   **MYD-1643: Checkout SOP for company deactivation**
    *   **Context:** Operational process.
    *   **Risk:** Low - Inconsistent company deactivation process.
    *   **Action:** Define and implement SOP for company deactivation.
    *   **Status:** pending
*   **MYD-1642: Create blueprints to prevent BDs from `closing won` when required fields are empty**
    *   **Context:** Data quality.
    *   **Risk:** Medium - Incomplete data when closing deals.
    *   **Action:** Implement blueprints to enforce required fields before "closing won".
    *   **Status:** pending
*   **MYD-1631: Deals Module Sync**
    *   **Context:** CRM integration.
    *   **Risk:** High - Inconsistent deal data between CRM and backend. This is a complex Epic.
    *   **Action:** Implement full sync of the Deals Module between CRM and backend.
    *   **Status:** pending
*   **MYD-1588: Investigate why some tally infos have no summary**
    *   **Context:** Data quality.
    *   **Risk:** Low - Incomplete tally information.
    *   **Action:** Investigate why some tally infos lack summaries.
    *   **Status:** pending
*   **MYD-1584: Guidance Dashboard APIs**
    *   **Context:** New feature.
    *   **Risk:** Low - Missing APIs for guidance dashboard.
    *   **Action:** Implement APIs for the guidance dashboard.
    *   **Status:** in_progress
*   **MYD-1582: Add detailed logging for SMS notifications**
    *   **Context:** Observability.
    *   **Risk:** Low - Lack of visibility into SMS notification details.
    *   **Action:** Implement detailed logging for SMS notifications.
    *   **Status:** pending
*   **MYD-1556: todo fix me: this should not be a long try catch**
    *   **Context:** Code quality.
    *   **Risk:** Low - Overly broad error handling, hiding actual issues.
    *   **Action:** Refactor the long try-catch block into more granular error handling.
    *   **Status:** pending
*   **MYD-1537: Organize payment_gateway.webhooks**
    *   **Context:** Code refactoring.
    *   **Risk:** Low - Untidy webhook code.
    *   **Action:** Organize payment gateway webhooks into logical namespaces.
    *   **Status:** pending
*   **MYD-1536: Organize mindyou.utils**
    *   **Context:** Code refactoring.
    *   **Risk:** Low - Untidy utility functions.
    *   **Action:** Organize `mindyou.utils` into specific namespaces (e.g., `mindyou.utils.session`, `mindyou.utils.session.cancelling`).
    *   **Status:** pending
*   **MYD-1526: DeprecationError: PdfFileReader is deprecated... Use PdfReader instead. (PDF Extraction)**
    *   **Context:** Sentry issue, deprecated library usage.
    *   **Risk:** Medium - Future compatibility issues, potential for breakage.
    *   **Action:** Update PDF extraction code to use `PdfReader` instead of `PdfFileReader`.
    *   **Status:** pending
*   **MYD-1525: "[api] # todo: convert this into a celery task so if it fails, it will not disrupt the whole process"**
    *   **Context:** Asynchronous processing.
    *   **Risk:** Medium - API failures disrupting the main process.
    *   **Action:** Convert the identified API call into a Celery task for asynchronous and fault-tolerant execution.
    *   **Status:** pending
*   **MYD-1473: """Perpetual"" available session for a B2C user"**
    *   **Context:** B2C billing logic bug.
    *   **Risk:** High - Users getting free sessions, revenue loss.
    *   **Action:** Investigate and fix the logic that grants "perpetual" available sessions to B2C users. This is a critical bug affecting revenue.
    *   **Status:** pending
*   **MYD-1469: QC-RGC Screening & Escalation**
    *   **Context:** Operational process.
    *   **Risk:** Low - Inefficient screening process.
    *   **Action:** Streamline QC-RGC screening and escalation.
    *   **Status:** pending
*   **MYD-1457: [celery] Email responsible team for users who attempted for gcash or credit card**
    *   **Context:** Observability.
    *   **Risk:** Low - Lack of visibility into payment attempts.
    *   **Action:** Implement Celery task to email team about failed payment attempts.
    *   **Status:** pending
*   **MYD-1442: Add/integrate warning message (transaction consumption) inside web and mobile**
    *   **Context:** User experience.
    *   **Risk:** Low - Users unaware of transaction consumption.
    *   **Action:** Add warning messages for transaction consumption.
    *   **Status:** pending
*   **MYD-1434: TODO: set own site setting for reschedules**
    *   **Context:** Configuration.
    *   **Risk:** Low - Inflexible reschedule settings.
    *   **Action:** Implement site-specific reschedule settings.
    *   **Status:** pending
*   **MYD-1413: add `session_warning_reschedule_within_hours`**
    *   **Context:** User experience.
    *   **Risk:** Low - Users unaware of reschedule warnings.
    *   **Action:** Implement `session_warning_reschedule_within_hours`.
    *   **Status:** pending
*   **MYD-1412: add `session_prevent_reschedule_within_hours` workflow**
    *   **Context:** Business logic.
    *   **Risk:** Medium - Reschedules within critical hours.
    *   **Action:** Implement workflow to prevent reschedules within a certain time window.
    *   **Status:** pending
*   **MYD-1408: ZOHO API revamp v3**
    *   **Context:** Zoho integration improvement.
    *   **Risk:** Medium - Outdated Zoho API integration.
    *   **Action:** Revamp Zoho API integration to v3.
    *   **Status:** pending
*   **MYD-1392: Log payment failed events**
    *   **Context:** Observability.
    *   **Risk:** Low - Lack of visibility into failed payments.
    *   **Action:** Log all failed payment events.
    *   **Status:** pending
*   **MYD-1379: To Redis or Not to Redis**
    *   **Context:** Architectural decision.
    *   **Risk:** Medium - Suboptimal caching/session management if not addressed.
    *   **Action:** Evaluate and decide on Redis implementation for caching and session management.
    *   **Status:** pending
*   **MYD-1357: "Voiding a reservation is also voiding a "PAID" transaction"**
    *   **Context:** Payment logic bug.
    *   **Risk:** High - Incorrect voiding of paid transactions, revenue loss.
    *   **Action:** Investigate and fix the logic to prevent voiding paid transactions when a reservation is voided. This is a critical bug.
    *   **Status:** pending
*   **MYD-1317: Filter out PSC17 in list of assessments page and results if age >= 18**
    *   **Context:** Compliance.
    *   **Risk:** Low - Displaying inappropriate assessments.
    *   **Action:** Implement age-based filtering for PSC17 assessment.
    *   **Status:** pending
*   **MYD-1298: Refund process upgrades in admin**
    *   **Context:** Admin tool improvement.
    *   **Risk:** Low - Inefficient refund process.
    *   **Action:** Upgrade the refund process in the admin panel.
    *   **Status:** pending
*   **MYD-1277: Linkable assessment and community**
    *   **Context:** UI/UX improvement.
    *   **Risk:** Low - Disconnected user experience.
    *   **Action:** Make assessments and community features linkable.
    *   **Status:** pending
*   **MYD-1269: Create a migration logic for practitioners for MYE x MYP**
    *   **Context:** Data migration.
    *   **Risk:** Low - Manual migration, potential for errors.
    *   **Action:** Create migration logic for practitioners between MYE and MYP.
    *   **Status:** pending
*   **MYD-1226: discourse and google analytics integration**
    *   **Context:** Analytics and community integration.
    *   **Risk:** Low - Missing analytics for Discourse.
    *   **Action:** Integrate Discourse with Google Analytics.
    *   **Status:** pending
*   **MYD-1210: Assessment Uploading in Admin**
    *   **Context:** Admin tool feature.
    *   **Risk:** Low - Manual assessment uploading.
    *   **Action:** Implement assessment uploading in the admin panel.
    *   **Status:** pending
*   **MYD-1185: completed refund request -> not automatically canceled**
    *   **Context:** Refund workflow bug.
    *   **Risk:** Medium - Inconsistent refund/cancellation status.
    *   **Action:** Ensure sessions are automatically cancelled upon completed refund requests.
    *   **Status:** pending
*   **MYD-1139, MYD-1136, MYD-1135, MYD-1134, MYD-1133: Cypress Test Upgrades v1 (PHQ9, Cancellation, Intake, Booking Flows)**
    *   **Context:** Test automation.
    *   **Risk:** Medium - Inadequate test coverage for critical flows.
    *   **Action:** Implement Cypress tests for PHQ9, 24-hour cancellation, intake, and booking flows.
    *   **Status:** pending
*   **MYD-1132: Cypress Test Upgrades v1**
    *   **Context:** Test automation.
    *   **Risk:** Medium - Inadequate overall test coverage.
    *   **Action:** Implement Cypress test upgrades.
    *   **Status:** pending
*   **MYD-1069: Rich text field in session notes**
    *   **Context:** Feature enhancement.
    *   **Risk:** Low - Limited formatting in session notes.
    *   **Action:** Implement rich text editor for session notes.
    *   **Status:** pending
*   **MYD-1045: [FEATURE] create a receipt/report for billable companies when limits reached**
    *   **Context:** Billing feature.
    *   **Risk:** Medium - Lack of billing transparency for companies.
    *   **Action:** Create receipts/reports for billable companies when limits are reached.
    *   **Status:** pending
*   **MYD-1030: one account technical discussion**
    *   **Context:** Technical discussion.
    *   **Risk:** Low - Unresolved architectural decisions.
    *   **Action:** Schedule and conduct technical discussion for "one account" feature.
    *   **Status:** blocked (by MYD-1029)
*   **MYD-1029: (AXA) One Account - Multiple Users (insurance companies)**
    *   **Context:** Complex user management for insurance companies.
    *   **Risk:** High - Incorrect user/account management for AXA.
    *   **Action:** Implement "one account - multiple users" for insurance companies. This is a complex Epic.
    *   **Status:** in_progress
*   **MYD-884: "[UPGRADE] Implement refresh token when "Keep me logged in" is checked if oauth2_enabled = true"**
    *   **Context:** Authentication improvement.
    *   **Risk:** Medium - Inconvenient user experience for long sessions.
    *   **Action:** Implement refresh token functionality for "Keep me logged in."
    *   **Status:** pending
*   **MYD-881: [UPGRADE] Use RDS for discourse community**
    *   **Context:** Infrastructure upgrade.
    *   **Risk:** Low - Suboptimal database for Discourse.
    *   **Action:** Migrate Discourse to use RDS.
    *   **Status:** pending
*   **MYD-826: Google service account file -> encrypted s3**
    *   **Context:** Security.
    *   **Risk:** High - Unencrypted service account files.
    *   **Action:** Migrate Google service account files to encrypted S3.
    *   **Status:** in_progress
*   **MYD-814: [FEATURE] Mood Tracker Graph Upgrades**
    *   **Context:** Feature enhancement.
    *   **Risk:** Low - Suboptimal mood tracker visualization.
    *   **Action:** Upgrade mood tracker graphs (monthly/weekly reports).
    *   **Status:** pending
*   **MYD-730: [FEATURE] Wordpress Tags Integration**
    *   **Context:** Feature enhancement.
    *   **Risk:** Low - Limited content categorization.
    *   **Action:** Integrate Wordpress tags.
    *   **Status:** pending
*   **MYD-729: Unit testing for Resources app**
    *   **Context:** Quality assurance.
    *   **Risk:** Medium - Insufficient test coverage for resources app.
    *   **Action:** Implement unit tests for the Resources app.
    *   **Status:** pending
*   **MYD-705: Upgrade docker local setup for oauth backend server**
    *   **Context:** Developer experience.
    *   **Risk:** Low - Inefficient local development environment.
    *   **Action:** Upgrade Docker local setup for OAuth backend.
    *   **Status:** pending
*   **MYD-699: Setup wordpress webhook for staging and production**
    *   **Context:** Integration.
    *   **Risk:** Medium - Stale Wordpress data if webhook is not set up.
    *   **Action:** Set up Wordpress webhooks for staging and production.
    *   **Status:** blocked (by MYD-682)
*   **MYD-595: Place province and city as a dropdown**
    *   **Context:** UI/UX improvement.
    *   **Risk:** Low - Manual entry of location data.
    *   **Action:** Implement dropdowns for province and city.
    *   **Status:** staging
*   **MYD-580: Reservation status update in admin page should also trigger transition effects**
    *   **Context:** Admin tool improvement.
    *   **Risk:** Low - Inconsistent status transitions in admin.
    *   **Action:** Implement transition effects for reservation status updates in admin.
    *   **Status:** staging
*   **MYD-532: all datetimes must be adjusted to user's timezone setting**
    *   **Context:** User experience.
    *   **Risk:** Medium - Incorrect display of times for users in different timezones.
    *   **Action:** Implement timezone adjustment for all datetimes.
    *   **Status:** pending
*   **MYD-440: Websockets for payments**
    *   **Context:** Real-time updates for payments.
    *   **Risk:** Low - Lack of real-time payment status updates.
    *   **Action:** Implement Websockets for real-time payment updates.
    *   **Status:** pending
*   **MYD-327: fix docker setup in oauth2.0 backend**
    *   **Context:** Developer experience.
    *   **Risk:** Low - Inefficient local development environment.
    *   **Action:** Fix Docker setup for OAuth2.0 backend.
    *   **Status:** pending
*   **MYD-248: [social media login] B2C Multiple Sign In Options**
    *   **Context:** Authentication feature.
    *   **Risk:** Medium - Limited sign-in options for B2C.
    *   **Action:** Implement multiple social media sign-in options for B2C.
    *   **Status:** blocked
*   **MYD-145, MYD-144, MYD-115: Coupon / Promo Upgrades**
    *   **Context:** Feature enhancement for promotions.
    *   **Risk:** Low - Limited promotional capabilities.
    *   **Action:** Implement coupon and promo upgrades.
    *   **Status:** pending
*   **MYD-125: Any psychs (list all available times)**
    *   **Context:** User experience.
    *   **Risk:** Low - Difficulty finding available psychologists.
    *   **Action:** Implement "Any psychs" option to list all available times.
    *   **Status:** pending
*   **MYD-32: integrate redis with the user online status**
    *   **Context:** Real-time feature.
    *   **Risk:** Low - Inaccurate user online status.
    *   **Action:** Integrate Redis for user online status.
    *   **Status:** pending
*   **MYD-27: Assessment feedbacks**
    *   **Context:** User feedback mechanism.
    *   **Risk:** Low - Lack of user feedback for assessments.
    *   **Action:** Implement assessment feedback mechanism (e.g., 5-star rating with text).
    *   **Status:** pending

## Low Priority - Future Enhancements

*   **MYD-3116: implement MY_SESB_8815**
    *   **Context:** New feature implementation.
    *   **Risk:** Low
    *   **Action:** Implement MY_SESB_8815.
    *   **Status:** to_do
*   **MYD-3115: implement MY_SESB_8816**
    *   **Context:** New feature implementation.
    *   **Risk:** Low
    *   **Action:** Implement MY_SESB_8816.
    *   **Status:** to_do
*   **MYD-3114: [error code] improvement for errors in sessions from user [frontend] [backend]**
    *   **Context:** Error messaging improvement.
    *   **Risk:** Low - Unclear error messages.
    *   **Action:** Improve error codes and messages for sessions on frontend and backend.
    *   **Status:** to_do
*   **MYD-3110: [after rescheduling details] add more details inside the modal**
    *   **Context:** UI/UX improvement.
    *   **Risk:** Low - Missing details in rescheduling modal.
    *   **Action:** Add more details to the rescheduling modal.
    *   **Status:** staging
*   **MYD-3109: [bug] practitioner image is shrunk on the booking details**
    *   **Context:** UI bug.
    *   **Risk:** Low - Suboptimal display of practitioner image.
    *   **Action:** Fix practitioner image size on booking details.
    *   **Status:** staging
*   **MYD-3105: Change contact added successfully -> Thank you for adding your contact! :D**
    *   **Context:** UI/UX copy change.
    *   **Risk:** Low - Suboptimal success message.
    *   **Action:** Update success message for contact addition.
    *   **Status:** staging
*   **MYD-3100: refreshes in sessions page makes hotline unavailable**
    *   **Context:** UI bug.
    *   **Risk:** Low - Hotline unavailable after refresh.
    *   **Action:** Fix hotline availability after refresh on sessions page.
    *   **Status:** staging
*   **MYD-3098: All null appointment type id in the session data should be filled up by the appointment type id practitioner default**
    *   **Context:** Data consistency.
    *   **Risk:** Low - Null appointment types.
    *   **Action:** Populate null appointment type IDs with practitioner defaults.
    *   **Status:** to_do
*   **MYD-3097: [booking] booking with an old account is failing**
    *   **Context:** Booking bug.
    *   **Risk:** Low - Old accounts unable to book.
    *   **Action:** Fix booking for old accounts.
    *   **Status:** to_do
*   **MYD-3092: [intern] generate wordclouds from https://github.com/amueller/word_cloud**
    *   **Context:** Data visualization.
    *   **Risk:** Low - Missing word cloud functionality.
    *   **Action:** Implement word cloud generation.
    *   **Status:** to_do
*   **MYD-3090: Feedback Improvement**
    *   **Context:** Feedback mechanism.
    *   **Risk:** Low - Suboptimal feedback process.
    *   **Action:** Improve the feedback mechanism.
    *   **Status:** to_do
*   **MYD-3088: [backend] automatically create a monthly sheet for mood tags and aspects - points system involved**
    *   **Context:** Reporting automation.
    *   **Risk:** Low - Manual mood report generation.
    *   **Action:** Automate monthly sheet creation for mood tags.
    *   **Status:** to_do
*   **MYD-3087: [frontend] feedback mechanism for mood tracker**
    *   **Context:** UI/UX improvement.
    *   **Risk:** Low - Missing feedback for mood tracker.
    *   **Action:** Implement frontend feedback mechanism for mood tracker.
    *   **Status:** to_do
*   **MYD-3086: [backend] Automatically create a monthly sheet for mood tracker**
    *   **Context:** Reporting automation.
    *   **Risk:** Low - Manual mood report generation.
    *   **Action:** Automate monthly sheet creation for mood tracker.
    *   **Status:** to_do
*   **MYD-3085: [backend] API to provide monthly mood tracker data analytics**
    *   **Context:** Reporting feature.
    *   **Risk:** Low - Missing API for mood tracker analytics.
    *   **Action:** Implement API for monthly mood tracker data analytics.
    *   **Status:** to_do
*   **MYD-3084: "[frontend] implement integration to sentry, with label frontend"**
    *   **Context:** Error tracking.
    *   **Risk:** Low - Missing frontend error tracking.
    *   **Action:** Implement Sentry integration for frontend.
    *   **Status:** to_do
*   **MYD-3083: Uptime Tracking**
    *   **Context:** Monitoring.
    *   **Risk:** Low - Lack of uptime tracking.
    *   **Action:** Implement uptime tracking for server, DNS, etc.
    *   **Status:** in_progress
*   **MYD-3080: [docker] [slack] [backend] [api] run on .yml**
    *   **Context:** DevOps automation.
    *   **Risk:** Low - Manual deployment.
    *   **Action:** Implement YAML-based deployment for backend API.
    *   **Status:** blocked
*   **MYD-3079: [docker] [slack] [frontend] [portal] run on .yml**
    *   **Context:** DevOps automation.
    *   **Risk:** Low - Manual deployment.
    *   **Action:** Implement YAML-based deployment for frontend portal.
    *   **Status:** blocked
*   **MYD-3078: [docker] [slack] transparency over builds; docker builds output in #tech-dump**
    *   **Context:** Observability.
    *   **Risk:** Low - Lack of visibility into build process.
    *   **Action:** Send Docker build output to #tech-dump Slack channel.
    *   **Status:** to_do
*   **MYD-3058: Duplicated Zoho links in the backend**
    *   **Context:** Data quality.
    *   **Risk:** Low - Duplicate Zoho links.
    *   **Action:** Remove duplicate Zoho links in the backend.
    *   **Status:** to_do
*   **MYD-3055: [wordpress] CSP fix for Allegis**
    *   **Context:** Security.
    *   **Risk:** Low - CSP issues for Wordpress.
    *   **Action:** Implement CSP fix for Wordpress (Allegis).
    *   **Status:** to_do
*   **MYD-3051: fix SaaSWebhookViewset**
    *   **Context:** Bug fix.
    *   **Risk:** Low - Malfunctioning SaaS webhook.
    *   **Action:** Fix `SaaSWebhookViewset`.
    *   **Status:** to_do
*   **MYD-3033: [oauth] expire token after 1 week**
    *   **Context:** Security.
    *   **Risk:** Low - Long-lived access tokens.
    *   **Action:** Implement 1-week expiry for OAuth tokens.
    *   **Status:** to_do
*   **MYD-3024: [gdoc] make sure local works**
    *   **Context:** Local development.
    *   **Risk:** Low - Google Docs integration not working locally.
    *   **Action:** Ensure Google Docs integration works in local environment.
    *   **Status:** to_do
*   **MYD-3023: remove .json private keys from /google folder -> use proper encryption and .env references**
    *   **Context:** Security.
    *   **Risk:** Medium - Private keys exposed.
    *   **Action:** Remove private keys from `/google` folder and use proper encryption and `.env` references.
    *   **Status:** to_do
*   **MYD-3019: [admin] company email - deactivation process is not updating zoho**
    *   **Context:** Zoho integration bug.
    *   **Risk:** Low - Inconsistent company email deactivation status.
    *   **Action:** Fix company email deactivation process to update Zoho.
    *   **Status:** to_do
*   **MYD-3018: "[admin] add a tooltip above practitioner types - if the rules are set for types in the company, then we need to set every type"**
    *   **Context:** UI/UX improvement.
    *   **Risk:** Low - Unclear rules for practitioner types.
    *   **Action:** Add tooltip for practitioner types in admin.
    *   **Status:** to_do
*   **MYD-3017: "[portal] cache problem on browser, logged in a distriphil - showed uprise survey and booking approval is on"**
    *   **Context:** Caching bug.
    *   **Risk:** Low - Incorrect content displayed due to caching.
    *   **Action:** Investigate and fix browser caching issues in the portal.
    *   **Status:** to_do
*   **MYD-2999: [sessions] add tracker on the client side to see why the session is canceled**
    *   **Context:** Analytics.
    *   **Risk:** Low - Lack of insight into session cancellation reasons.
    *   **Action:** Add client-side tracker for session cancellation reasons.
    *   **Status:** to_do
*   **MYD-2995: [compliance] access control management policy**
    *   **Context:** Compliance.
    *   **Risk:** Medium - Non-compliance with access control policy.
    *   **Action:** Implement access control management policy.
    *   **Status:** to_do
*   **MYD-2994: [aws] investigate AWS guardduty incidents**
    *   **Context:** Security.
    *   **Risk:** Low - Uninvestigated security incidents.
    *   **Action:** Investigate AWS GuardDuty incidents.
    *   **Status:** to_do
*   **MYD-2992: Implement AFFiene to replace lucidchart or miro board**
    *   **Context:** Tooling change.
    *   **Risk:** Low - Inefficient diagramming tools.
    *   **Action:** Implement AFFiene as a replacement for Lucidchart/Miro.
    *   **Status:** to_do
*   **MYD-2991: [aws] setup stream log for b2c celery to cloudwatch**
    *   **Context:** Observability.
    *   **Risk:** Low - Missing logs for B2C Celery.
    *   **Action:** Setup CloudWatch stream logs for B2C Celery.
    *   **Status:** to_do
*   **MYD-2990: [aws] setup stream log for b2b celery to cloudwatch**
    *   **Context:** Observability.
    *   **Risk:** Low - Missing logs for B2B Celery.
    *   **Action:** Setup CloudWatch stream logs for B2B Celery.
    *   **Status:** to_do
*   **MYD-2989: [aws] setup stream log for b2c api to cloudwatch**
    *   **Context:** Observability.
    *   **Risk:** Low - Missing logs for B2C API.
    *   **Action:** Setup CloudWatch stream logs for B2C API.
    *   **Status:** to_do
*   **MYD-2988: [aws] setup stream log for b2b api to cloudwatch**
    *   **Context:** Observability.
    *   **Risk:** Low - Missing logs for B2B API.
    *   **Action:** Setup CloudWatch stream logs for B2B API.
    *   **Status:** to_do
*   **MYD-2987: [aws] [elasticache] [stg] apply updates for upgrades**
    *   **Context:** Infrastructure maintenance.
    *   **Risk:** Low - Outdated ElastiCache.
    *   **Action:** Apply updates for ElastiCache upgrades in staging.
    *   **Status:** to_do
*   **MYD-71: Ensure liveness and updated data in resources**
    *   **Context:** Data quality.
    *   **Risk:** Medium - Stale resource data.
    *   **Action:** Implement mechanisms to ensure liveness and updated data in resources.
    *   **Status:** in_progress (Parent for MYD-699)

## Risks & Dependencies

*   **Zoho/Acuity Integrations (High Risk):** Multiple high-priority bugs are related to Zoho and Acuity integrations. These require careful investigation and robust error handling to prevent data loss, desyncs, and payment issues. Prioritize these to ensure core business functions are stable.
*   **Security (Highest Risk):** MYD-2255 (User data in local storage) and MYD-3023 (JSON private keys) are significant security concerns. Continue to treat these with high urgency.
*   **Payment & Billing (High Risk):** MYD-2699, MYD-2698, MYD-2612, MYD-2223, MYD-1894, MYD-1680, MYD-1473, MYD-1357, MYD-1335 are all related to payment processing, billing, refunds, and session consumption. Errors here directly impact revenue and customer trust.
*   **User Onboarding/Access (Medium Risk):** MYD-2819, MYD-2813, MYD-2339, MYD-2321, MYD-1852 affect users' ability to sign up, log in, and access the platform.
*   **Data Consistency (Medium Risk):** Issues like duplicate data (MYD-3058, MYD-2922, MYD-2902, MYD-2281, MYD-1877), data desyncs (MYD-2831, MYD-2822), and missing data (MYD-2952) can lead to operational headaches and incorrect reporting.
*   **Large Epics (Complexity Risk):** MYD-3118 (E2E Revamp), MYD-1717 (NLE/NLS Flow), MYD-1631 (Deals Module Sync), MYD-1029 (One Account - Multiple Users) are large, complex initiatives. These should be broken down further, with clear milestones and continuous testing to mitigate execution risk.
*   **Technical Debt (Medium-Long Term Risk):** Items like Typescript conversion, serializer cleanup, and deprecated package removal are important for long-term maintainability and reducing future regret. While not immediate blockers, they contribute to the "catastrophic tomorrow" if ignored.

## Deferred / Questionable

*   **MYD-682: Ensure liveness and updated data in resources**
    *   **Status:** In Progress (Parent for MYD-699), but its own action is not clearly defined beyond being a parent. Needs re-evaluation.
*   **MYD-3083: Uptime Tracking**
    *   **Status:** In Progress, but details are broad. Needs more specific tasks.
*   **MYD-1029: (AXA) One Account - Multiple Users (insurance companies)**
    *   **Status:** In Progress, but also blocked by a "technical discussion" (MYD-1030). The dependency needs to be resolved to unblock progress.
*   **MYD-1715: Social Media Logins**
    *   **Status:** In Progress, but also has child tasks (MYD-1748, MYD-1747) that are themselves pending/blocked.

---

**Next Steps:**

1.  **Review with Stakeholders:** Share this `todo.md` with relevant teams (Product, Engineering, Operations, Support) to ensure alignment on priorities and understanding of risks.
2.  **Deep Dive into High Priority Bugs:** For each high-priority bug, assign an owner and ensure a detailed investigation plan is in place to identify the root cause and implement a robust fix.
3.  **Break Down Epics:** For large epics like MYD-1717 and MYD-1631, work with the respective teams to break them down into smaller, actionable stories with clear definitions of done.
4.  **Allocate Resources:** Ensure adequate engineering resources are allocated to address the high-priority bugs and critical technical debt items.
5.  **Monitor Progress:** Regularly review the status of these tasks and update `todo.md` to reflect progress, new discoveries, and any shifts in priority.
