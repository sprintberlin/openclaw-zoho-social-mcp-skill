## Description: <br>
Connects an agent to Zoho Social through MCP so it can list portals, brands, and channels, inspect drafts and schedules, upload media, and use mcporter-based helper scripts for common Social operations. <br>

This skill is ready for commercial/non-commercial use. <br>

## Publisher: <br>
[sprintcx](https://clawhub.ai/user/sprintcx) <br>

### License/Terms of Use: <br>
MIT <br>


## Use Case: <br>
Developers and social operators use this skill to connect an agent to Zoho Social via MCP, configure least-privilege action profiles, browse portals and brands, inspect posts, and upload media through mcporter. <br>

### Deployment Geography for Use: <br>
Global <br>

## Known Risks and Mitigations: <br>
Risk: The ZOHO_SOCIAL_MCP_URL endpoint is credential-bearing and could expose Social access if echoed, logged, or shared. <br>
Mitigation: Treat the MCP URL like a password, avoid printing the full value, and enable only the Actions required for the chosen profile. <br>
Risk: Helper scripts pass the credential-bearing MCP endpoint to mcporter, so local process visibility and logs should be treated carefully. <br>
Mitigation: The scripts call mcporter directly without shell expansion and never print ZOHO_SOCIAL_MCP_URL intentionally. Run them only on trusted systems. <br>
Risk: Read-write Zoho Social actions can publish or delete scheduled posts if enabled on the MCP server. <br>
Mitigation: Start with the social-viewer profile for lookup work. Use social-creator for drafts and media. Keep social-publisher for scheduling and live publish. Keep deleteSocialSchedule disabled unless explicitly required. <br>
Risk: Truncated base64 image payloads can produce corrupt media-library assets while the MCP call still reports success. <br>
Mitigation: Use scripts/upload_media.py so the complete data-URI payload is sent, treat a missing file ID as failure, and re-list the library. <br>
Risk: Zoho Social contains customer content and publishing credentials. <br>
Mitigation: Load only required records and never copy post text, media, or IDs into chats, logs, or repositories. <br>


## Reference(s): <br>
- [Zoho Social MCP ClawHub page](https://clawhub.ai/sprintcx/skills/zoho-social-mcp) <br>
- [GitHub source repository](https://github.com/sprintberlin/openclaw-zoho-social-mcp-skill) <br>
- [Zoho MCP portal](https://mcp.zoho.eu) <br>


## Skill Output: <br>
**Output Type(s):** [guidance, shell commands, configuration, code] <br>
**Output Format:** [Markdown guidance with bash, JSON, and Python examples] <br>
**Output Parameters:** [1D] <br>
**Other Properties Related to Output:** [Requires ZOHO_SOCIAL_MCP_URL, a named profile, or a one-off endpoint; bundled helper scripts can print table or JSON output from Zoho Social MCP calls.] <br>

## Skill Version(s): <br>
1.0.0 <br>

## Ethical Considerations: <br>
Users should evaluate whether this skill is appropriate for their environment, review any generated or modified files before relying on them, and apply their organization's safety, security, and compliance requirements before deployment. <br>
