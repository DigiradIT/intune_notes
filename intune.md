# Intune

Intune for deploying hardware refresh to TTG organization as a whole.

## Benefits
Over all there is a strong operational return on **homogenous** computing environments.  Reducing the number of configurations in an environment reduces the complexity of solutions thereby increasing the efficency of support staff.  

**Long Explanation of My Reasoning for Above**
Operations can be thought of as a series of service events (either planned maintenance, projects, break-fix, etc.), which must be paired with a solution.  The amount of unique solutions needed is, roughly, equal to the number of computing environments (special laptop a, snowflake server y, etc.) multiplied by the number of event types.  Given that we have strong control of the number of unique computing environments through standardizing deployments and very little over the variety of service events that can occur (it is difficult to refuse to help a user with an event, even if it is unusual) we can reduce the number of solutions by standardizing systems.  With a smaller number of solutions for any given set of problems we can either increase the types of service events we can respond to and/or decrease the time and effort needed to find a solution to any problem.


Through this deployment we will also be able to enforce uniform connectivity, visibility, and user experience on TTG devices.


## Execution

Once we have determined a process in testing we will only need to role this out on computers for the hardware refresh.  Some high level ideas for this would be to do staggered deploys for sites or zones:
  1. Deploy to "champion" and provide close supervision.  Concentrate on selling the solution and listening for improvements.
  2. Deploy to the rest of the site with the help of the champion, stagger these deployments to saturate with IT staff support.

## Testing and Questions

### Sign-in and auth up
Sign-in and get pim access.  Document exactly what perms are needed.

**Notes**
For me activating the role and putting in a note takes about 5 minutes (counting downtime waiting for the role to apply).  I haven't had issues with Intune not recognizing my PIM role.

**Questions**
1. [ ]?Can we make this any faster? -> Patrick
2. [ ]?Are staff comfortable with PIM as is? -> Ken
3. [ ]?Who should have Intune admin role in PIM? -> Ken
4. [ ]?Will this access be part of our access review process? -> Emin 
5. [ ]?Can Security access with current permissions? -> Emin (accepted 5/21)

### Check machine status
Are current computers joined showing online.  Ken and Patrick should each have a joined machine.

**Notes**
Both Machines show up, but mine is taking some time to update it's last check-in time.  Something to consider when looking for non-compliant computers.

We can route logs to log analytics.  I have configured all logs to be shipped for now [MSFT Docs](https://learn.microsoft.com/en-us/mem/intune/fundamentals/review-logs-using-azure-monitor).



**Questions**
1. [x]?Ken and patrick PCs joined and in sync? -> Patrick, Ken
2. [x]?Can this report back to Log Analytics? -> Patrick, Emin
2. [ ]?Are logs showing up? -> Emin (asked via Teams 5/21)

### Simple GPOS 
Can we push simple GPOs, if not reconsider Intune.

**Notes**
Endpoint policy is applied, but the status of the devices in reporting is not 
Bitlocker worked on my machine and on Ken's test machine.

Devices have the endpoint policy applied but when I check their endpoint status in reporting it shows their MDE status as not enrolled.  I don't know if this is significant, but we should look into it further.

Intune must be connected with Microsoft Defender, I enabled this following [MSFT Instructions](https://learn.microsoft.com/en-us/mem/intune/protect/advanced-threat-protection-configure#connect-microsoft-defender-for-endpoint-to-intune).  I needed global admin active to make the change.

Intune is now connected to MSFT defender and I've enabled EDR.  It will take time for this setting to make it out to the endpoints.

Having issues with performing actions on my machine:
  - Quick scan for defender is stuck in pending.
  - Collect diagnostics is stuck in pending

Created a policy for setting a login banner, but it has not been applied to my machine after two reboots.  Will give it some more time to see if it applies.  I am on a reliable network connection.

1. [x]Bitlocker
2. [ ]Endpoint Security enrollment/configuration.
3. [ ]Login Banner 
4. [ ]Dekstop Shortcuts
5. [ ]Browser Config
6. [ ]Default programs
7. [ ]Logging
8. [ ]Security group pol. e.g. Log retention, Log level

**Questions**
1. [ ]?Rules of engagement for setting these up.  Is this help desk level?  ITS level?  etc.? -> Vince, Ken
2. [ ]?Scoping of policy applicatoin? -> Patrick, Adrian 

### First LoB Apps
We need to see if we can get essential and/or simple applications to install.  If we can't manage this than we need to reconsider Intune.

1. [ ]Filemaker
2. [ ]Desktop office suite

**Questions**
1.  ?What is the process, who should be able to do it? -> Ken, Adrian
2.  ?Uninstall, easy, hard, impossible??? -> Patrick, Ken

### MSFT Remote Support
Can we enroll in remote support and request/join systems?  Is the experience comprable to Bomgar from a **frustrated user** perspective - no technical jargon, is this the same or easier for someone who doesn't care how it's done?

**Questions**
1.  ?Can we run remote scripts (not that important can be accomplished in other ways, but nice)? -> Adrian, Ken
2.  ?Can this be used to remote into non-corporate devices (e.g. for installed camera support)? -> Adrian, Ken

### TailScale Installation
Proper install of TailScale with network joining experience that is accessible to a user.  Connecting should be as **simple or simpler** for a hurried user as the current experience? 
1. [ ]Connect and verify configuration

**Tasks**
- [ ]Emin permissions for tailscale.  Need to research level required and submit change request and get it approved.

**Questions**
1.[ ]?Do we like our device groups as they are now or do we want to narrow down, should use our connection logging in tailscale for this? -> Patrick, Ken, Emin
2.[ ]?Can we think of any groups that don't need connection? -> Ken, Vince
3.[ ]?Can we think of any groups that need more connectivity (ScImage service)? -> Ken, Vince

### Lost/Stolen Process
Run through process for lost or stolen device.  Use the existing procedure as a guide.  Can we satisfy the same things using Intune in place of EMS?
### In-place redeploy
### Recover and Decom
### Fresh Deploy from Vendor 
Should be usable to a user with the assistance of a supervisor.  Should take no longer than 1 hour to complete.  Think about laziness here, are there setup steps that can be done after the first login has completed?

## General Lines of Inquiry 
- Security DWMs through Intune, can we support our current list?  If not are the unsupported ones unessential -> Emin (talked about this with Emin on 5/22)
- Local session duration - how long until all remembered credentials are wiped or invalidated?   Can we setup a deadman's switch here? -> Emin, Patrick
- Can we use this for server monitoring and update? -> Ken, Adrian
- Deadman switch for complete wipe (will have significant security and operational impact, run through with Ken)?  -> Emin, Patrick, Ken


## Help Desk Considerations
- We will have a lot of information about comeuters in the field on a daily basis.  How can we use this to reduce ticket load?  There **must** be ways we can perform preventative maintenance.
- Identifying non-compliant computers.
- Remote support options - how can we make this experience quicker and easier?

## Security Considerations
- How can we use increased information for access control.  Can we use the Intune status of a machine in our PIM policies?
- How deeply can we integrate into Log Analytics?  What data is interesting?
- Testing vulnerability scanning - can we report on this? -> Emin (mentioned in meeting on 5/22)

## Management Considerations
- Reporting and visibility - are there metrics or trends that would be valuable to internal stake holders?
- Same for external - for example if we could promise complete management of deployed computers through intune to a lease client would that help lease negotiations?  We could offer logs from Intune for their compliance team.
- Can this help manufacturing - could we deploy our machines in Kiosk mode connected to Intune?  Remote support, licensing, and maintenance would be **much** easier.  Downside is that we have deeper access to client computer, but we can demonstrate compliance using logging, etc.
