# Investigation Summary

## Incident Type

Potential brute-force authentication activity detected during a Windows security log investigation.

## Log Source

Windows Security Event Logs analyzed in Splunk.

## Event ID

**4625 - Failed Logon**

Event ID 4625 was used to identify unsuccessful authentication attempts and investigate repeated login failures.

## What I Investigated

During the investigation, I:

- Identified Windows Event ID 4625 failed login events.
- Extracted the target account involved in the failed attempts.
- Extracted the process responsible for the authentication activity.
- Analyzed the number of failed login attempts for each account.
- Reviewed the activity over time to identify repeated attempts within a short period.
- Created a threshold-based detection rule for potential brute-force activity.
- Built a Splunk dashboard to visualize the investigation results.

## Observed Activity

The lab dataset contained multiple failed authentication attempts against a test account.

The events included Windows Security Event ID 4625 and OpenSSH-related authentication activity. The repeated failures provided a useful scenario for investigating whether the activity could represent brute-force behavior.

The available log data did not provide complete source network information for every event, so the activity was evaluated using the fields that were available in the captured logs.

## Detection Logic

For this lab, I used a simple threshold-based detection approach:

**5 or more failed login attempts for the same target account within a 5-minute window were treated as suspicious activity requiring further investigation.**

This threshold is specific to the lab and should not be considered a universal production rule. In a real SOC environment, the threshold would depend on the organization's normal authentication behavior and additional context.

## Analyst Interpretation

A high number of failed authentication attempts within a short period can have several possible explanations, including:

- Brute-force authentication
- Password spraying
- Incorrect or expired credentials
- Credential misuse
- Misconfigured applications or services
- Legitimate user authentication problems

Therefore, repeated failed logins should be treated as a **potential security event**, rather than immediately being classified as a confirmed attack.

Additional logs and context would be required before confirming malicious activity.

## Recommended SOC Response

If this activity were observed in a real environment, the next steps would be:

1. Identify and validate the affected user account.
2. Review the source IP or network information when available.
3. Check authentication events immediately before and after the detected activity.
4. Investigate the process responsible for the authentication attempts.
5. Determine whether the activity is expected or related to a legitimate service/user.
6. Look for additional indicators of compromise or suspicious authentication activity.
7. Escalate the incident according to the organization's SOC and incident-response procedures if malicious activity is confirmed.

## Conclusion

This investigation demonstrates how Splunk can be used to collect, search, extract, and analyze Windows authentication events.

By starting with Event ID 4625 and progressively analyzing the account, process, frequency, and timing of failed logins, I created a basic workflow for identifying and investigating potential brute-force authentication activity.

The project helped me practice practical SOC skills including **Splunk SPL, Windows Event Log analysis, field extraction, authentication monitoring, threshold-based detection, and security dashboard creation.**
