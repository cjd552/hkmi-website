Cloud computing
* Low cost
* Elastic - allows for swapping to larger amount of resources, temporarily assigning more in a particular situation, proper setup allows for handover to another server in event of a crash
* Flexible - safety precautions in place in case of hardware failure, everything is done via AWS API
* Secure

Azure - best for Windows
AWS - most popular overall

worries of on-premises vs cloud
* how many resources are being used
* does it support current / future use cases
* cost of buying a server
* security updates (these are automatic by default on cloud)
* port forwarding

a random availability zone is offered to you, which has its own databaase. it is mirrored with at least 2 backups, used to restore damage to the affected zone.

IAM - control user and service accounts. All Free features (except fine-grained audit log)

IAM Permissions can now be set in editor, or with JSON

users inherit permissions from any group(s) they are in, the one with the highest perms is taken

policy -> user, role -> service (what other services it can access)

root user -> for building service
IAM user -> for accessing service
as soon as IAM user is compromised, root user can kill it off

Mobile app is much faster than email for notifications on usage limits (by the time they warn you it's 70% used, you might've already used your allowance)