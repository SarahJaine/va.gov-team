## External Auth Data - Queries Defined

- Monthly Active Users
- Total Authentications Per Month
- Credential Preference Per Month
   - Which CSP are people using to login per month?

| Data | Metrics or Logs | Query | Link to DD Widget | Link to SiS Code | Link to SSOe Code |
| --- | --- | --- | --- | --- | --- |
| Monthly Active Users | Logs | (signincontroller (callback OR refresh)) OR "LOGIN_STATUS_SUCCESS" env:eks-prod | [Link](https://vagov.ddog-gov.com/dashboard/e3q-6kp-9r4/vagov-identity-stats-public?fromUser=false&refresh_mode=paused&view=spans&from_ts=1714327639555&to_ts=1716919639555&live=false&tile_focus=1435425616298618) | [SiS Log](https://github.com/department-of-veterans-affairs/vets-api/blob/master/app/controllers/v0/sign_in_controller.rb#L311) | [SSOe Log](https://github.com/department-of-veterans-affairs/vets-api/blob/master/app/controllers/v1/sessions_controller.rb#L391) // [Payload](https://github.com/department-of-veterans-affairs/vets-api/blob/master/app/controllers/concerns/authentication_and_sso_concerns.rb#L141) |
| Total Authentications | Metrics | "sum:vets_api.statsd.api_auth_login_success{type IN (dslogon,mhv,idme,logingov) AND (env:eks-prod)} by {type}.as_count()” + "sum:vets_api.statsd.api_sis_callback_success{(env:eks-prod)} by {type}.as_count()” | [Link](https://vagov.ddog-gov.com/dashboard/e3q-6kp-9r4/vagov-identity-stats-public?fromUser=true&refresh_mode=paused&view=spans&from_ts=1716988743250&to_ts=1717003143250&live=false&tile_focus=7062638735213996) | [SiS Metric](https://github.com/department-of-veterans-affairs/vets-api/blob/master/app/controllers/v0/sign_in_controller.rb#L312) | [SSOe Metric](https://github.com/department-of-veterans-affairs/vets-api/blob/master/app/controllers/v1/sessions_controller.rb#L277) |
| Credential Preference | Metrics | Too long to list. The metric applied is `(sis_callback_success for CREDENTIAL + api_auth_login_success for CREDENTIAL) / (TOTAL sis_callback_success + TOTAL api_auth_login_success)` | [Link](https://vagov.ddog-gov.com/dashboard/e3q-6kp-9r4/vagov-identity-stats-public?fromUser=true&refresh_mode=paused&view=spans&from_ts=1716988743295&to_ts=1717003143295&live=false&tile_focus=7405270615721338) | Same as total authentications | Same as total authentications |

[Datadog Group of widgets](https://vagov.ddog-gov.com/dashboard/e3q-6kp-9r4/vagov-identity-stats-public?fromUser=false&refresh_mode=paused&view=spans&from_ts=1714327639555&to_ts=1716919639555&live=false&tile_focus=1435425616298618)
