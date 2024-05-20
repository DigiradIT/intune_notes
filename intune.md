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

**Questions**
1. [ ]?Can we make this any faster? -> Patrick
2. [ ]?Are staff comfortable with PIM as is? -> Ken
3. [ ]?Will this access be part of our access review process? -> Emin

### Check machine status
Are current computers joined showing online.  Ken and Patrick should each have a joined machine.

**Questions**
1. [ ]?Ken and patrick PCs joined and in sync? -> Patrick, Ken
2. [ ]?Can this report back to Log Analytics? -> Patrick, Emin

### Simple GPOS 
Can we push simple GPOs, if not reconsider Intune.:
1. [ ]Bitlocker
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
- Security DWMs through Intune, can we support our current list?  If not are the unsupported ones unessential -> Emin
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

## Management Considerations
- Reporting and visibility - are there metrics or trends that would be valuable to internal stake holders?
- Same for external - for example if we could promise complete management of deployed computers through intune to a lease client would that help lease negotiations?  We could offer logs from Intune for their compliance team.
- Can this help manufacturing - could we deploy our machines in Kiosk mode connected to Intune?  Remote support, licensing, and maintenance would be **much** easier.  Downside is that we have deeper access to client computer, but we can demonstrate compliance using logging, etc.
