# Streamlining-ticket-assignment-for-efficient-support-operations
Project: Streamlining Ticket Assignment for Efficient Support Operations

Objective This project's objective is to deploy an automated ticket routing system within ABC Corporation's ServiceNow instance. The primary goal is to enhance operational efficiency by ensuring support tickets are accurately and automatically assigned to the correct specialized teams. This automation is designed to minimize resolution delays, improve resource allocation, and ultimately increase customer satisfaction.

Implementation Steps

User Creation Access ServiceNow. Navigate to All → System Security → Users. Select New to create a user, populate the required details, and click Submit. Repeat this process to create the second required user.

Group Creation Access ServiceNow. Navigate to All → System Security → Groups. Select New, enter the group's details, and click Submit. Repeat for the second required group.

Role Creation Access ServiceNow. Navigate to All → System Security → Roles. Select New, define the role details, and click Submit. Repeat to create the second role.

Table Creation Access ServiceNow. Navigate to All → System Definition → Tables. Select New and configure the table with the following details:

Label: Operations Related

Enable Create module & Create mobile module

New menu name: Operations Related

Add all required table columns.

Click Submit.

Choices for Issue Field (via Form Design): Configure the 'Issue' field on the new table's form with the following choice options:

Unable to login to platform

404 Error

Regarding Certificates

Regarding User Expired

Assign Roles & Users to Groups

Certificates Group:

Navigate to the Certificates Group record (All → System Security → Groups).

In the Group Members related list, add Katherine Pierce.

In the Roles related list, assign Certification_Role.

Platform Group:

Navigate to the Platform Group record (All → System Security → Groups).

In the Group Members related list, add Manne Niranjan.

In the Roles related list, assign Platform_Role.

Assign Roles to Table Access the Operations Related table definition (All → System Definition → Tables). In the Application Access tab:

For Read Operation: Require Platform_Role and Certification_Role.

For Write Operation: Require Platform_Role and Certification_Role.

Create ACL (Access Control List) Navigate to All → System Security → ACL.

Select New to create a new Access Control List.

In the Requires Role list, add the Admin Role.

Create 4 distinct ACLs as needed for the required fields to secure the table.

Flow Designer – Ticket Assignment Flow

Flow 1: Regarding Certificates

Open Flow Designer and create a New Flow.

Flow Name: Regarding Certificate

Application: Global

Run As: System User

Trigger: Record Created or Updated on the Operations Related table.

Condition: [Issue] [is] [Regarding Certificates]

Action: Update Record on the triggering record.

Field: [Assigned to group] → Value: [Certificates]

Save and Activate the flow.

Flow 2: Regarding Platform

Open Flow Designer and create a New Flow.

Flow Name: Regarding Platform

Application: Global

Run As: System User

Trigger: Record Created or Updated on the Operations Related table.

Conditions (OR):

[Issue] [is] [Unable to login to platform]

[Issue] [is] [404 Error]

[Issue] [is] [Regarding User Expired]

Action: Update Record on the triggering record.

Field: [Assigned to group] → Value: [Platform]

Save and Activate the flow.

📂 Project Structure

ABC-Ticket-Routing/
│
├── Users/
│   ├── Katherine Pierce (Certificate group)
│   ├── Manne Niranjan (Platform group)
│
├── Groups/
│   ├── Certificates Group
│   ├── Platform Group
│
├── Roles/
│   ├── Certification_role
│   ├── Platform_role
│
├── Tables/
│   ├── u_operations_related
│   │   ├── Issue (Choice field)
│   │   ├── Assigned to Group
│   │   └── Other custom columns
│
├── ACLs/
│   ├── Read access
│   ├── Write access
│   ├── Field-level restrictions
│
├── Flows/
│   ├── Regarding Certificate → Assigns to Certificates Group
│   └── Regarding Platform → Assigns to Platform Group
Outcome The resulting automated system within ServiceNow delivers the following outcomes:

Automatic routing of tickets to the correct specialized support groups.

Minimized delays in issue resolution.

Enhanced customer satisfaction through faster response times.

Efficient utilization of support department resources.
