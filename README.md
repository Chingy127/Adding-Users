<img width="900" alt="Adding Active Directory Users and Admins" src="images/Adding Users.jpeg">

<br>

<h2>Creating Domain Admins and Domain Users</h2>

<p>
After deploying Active Directory, administrators can begin organizing the directory structure and creating domain users. In this lab, Organizational Units (OUs) are created to separate administrative accounts from regular employee accounts.
</p>

<br>

<h3>Creating Organizational Units</h3>

<p>
Within the <strong>Active Directory Users and Computers</strong> console, right-click the domain and navigate to:
</p>

<p>
<strong>New → Organizational Unit</strong>
</p>

<p>
<img width="1400" alt="Creating Organizational Units in Active Directory" src="images/01-AD-Adding-Users.png">
</p>

<p>
Organizational Units allow administrators to logically organize users, computers, and other objects within the domain. This structure is commonly used in enterprise environments to separate departments, administrative accounts, and security policies.
</p>

<br>

<h3>Creating Admin and Employee Containers</h3>

<p>
Two Organizational Units are created to organize accounts within the environment.
</p>

<p>
<img width="1400" alt="Organizational units for admins and employees" src="images/02-AD-Adding-Users.png">
</p>

<p>
The following OUs are created:
</p>

<ul>
<li><strong>_ADMINS</strong> – used to store domain administrator accounts</li>
<li><strong>_EMPLOYEES</strong> – used to store standard domain user accounts</li>
</ul>

<p>
This structure allows administrators to apply different security policies and permissions to different groups of users.
</p>

<br>

<h3>Creating a New Domain Administrator</h3>

<p>
Next, a domain administrator account is created inside the <strong>_ADMINS</strong> organizational unit.
</p>

<p>
Right-click the <strong>_ADMINS</strong> OU and select:
</p>

<p>
<strong>New → User</strong>
</p>

<p>
<img width="1400" alt="Creating a new Active Directory user" src="images/03-AD-Adding-Users.png">
</p>

<p>
The administrator account is configured with the name <strong>Jane Gray</strong>.
</p>

<br>

<h3>Verifying the New Administrator Account</h3>

<p>
After completing the user creation wizard, the new account appears inside the <strong>_ADMINS</strong> organizational unit.
</p>

<p>
<img width="1400" alt="New domain admin user Jane Gray created" src="images/04-AD-Adding-Users.png">
</p>

<p>
At this stage, the account exists in Active Directory but does not yet have administrative privileges.
</p>

<br>

<h3>Granting Domain Administrator Privileges</h3>

<p>
To grant administrative permissions, the user must be added to the <strong>Domain Admins</strong> security group.
</p>

<p>
Open the user properties and navigate to the <strong>Member Of</strong> tab.
</p>

<p>
<img width="1400" alt="Adding user to Domain Admins group" src="images/05-AD-Adding-Users.png">
</p>

<p>
The account is added to the following groups:
</p>

<ul>
<li>Domain Admins</li>
<li>Domain Users</li>
</ul>

<p>
Membership in the <strong>Domain Admins</strong> group provides full administrative control across the Active Directory domain.
</p>

<br>

<h3>Logging in with the New Domain Administrator</h3>

<p>
After the administrator account is created, it can be used to log into domain-joined systems. The login format uses the domain name followed by the username.
</p>

<p>
<img width="1400" alt="Logging in using domain administrator credentials" src="images/06-AD-Adding-Users.png">
</p>

<p>
Example login format:
</p>

<pre>
mydomain.com\jane_admin
</pre>

<p>
Successful authentication confirms that the Active Directory domain controller is functioning correctly and that domain accounts can authenticate to systems within the environment.
</p>

<br>

<h3>Lab Outcome</h3>

<p>
At this stage the Active Directory environment now includes:
</p>

<ul>
<li>A functional Domain Controller</li>
<li>Organizational Units for administrative and employee accounts</li>
<li>A domain administrator account</li>
<li>Working domain authentication</li>
</ul>

<p>
This environment can now be expanded by joining client machines to the domain and generating additional user accounts to simulate a real enterprise network.
</p>

<h2>
  <img src="images/07-AD-Adding-Users.png" alt="Active Directory Client Domain Join" width="40" style="vertical-align: middle; margin-right: 10px;">
  Joining the Client Computer to the Domain
</h2>

<p>
This section walks through how the client machine is joined to the Active Directory domain that was created on the Domain Controller. 
Once a computer joins the domain, it can authenticate with domain accounts instead of only using local accounts on that machine.
This is important in enterprise environments because it allows centralized management, easier user access control, and domain-based authentication across multiple systems.
</p>

<p>
At this stage of the lab, the Domain Controller has already been configured and the <strong>mydomain.com</strong> domain already exists.
Now the goal is to connect the client workstation to that domain so it becomes part of the Active Directory environment.
</p>

<hr>

<h3>Step 1: Change the Client from a Workgroup Member to a Domain Member</h3>

<p>
On the client machine, open the system settings that allow you to rename the computer or change its network membership.
This brings up the <strong>Computer Name/Domain Changes</strong> window.
</p>

<p>
In this screen, the workstation name is shown as <strong>Client-01</strong>.
Under the <strong>Member of</strong> section, select <strong>Domain</strong> instead of <strong>Workgroup</strong>.
Then enter the domain name:
</p>

<pre>mydomain.com</pre>

<p>
This tells Windows that instead of operating as an isolated standalone machine, the computer should attempt to join and trust the Active Directory domain managed by the Domain Controller.
</p>

<p>
<img src="images/07-AD-Adding-Users.png" alt="Entering mydomain.com in the domain join box" width="900">
</p>

<p>
After clicking <strong>OK</strong>, Windows begins the process of contacting the Domain Controller to request domain membership.
</p>

<hr>

<h3>Step 2: Authenticate with an Account That Has Permission to Join the Domain</h3>

<p>
After entering the domain name, Windows prompts for credentials.
This happens because only authorized domain accounts can add computers to the domain.
If anyone could join machines freely, it would create a major security issue.
</p>

<p>
The credentials entered here must belong to an account with permission to join computers to <strong>mydomain.com</strong>.
In most beginner labs, this is usually the domain admin account or another account that has been delegated permission to add machines.
</p>

<p>
This credential prompt is asking for:
</p>

<ul>
  <li><strong>User name</strong> of an authorized domain account</li>
  <li><strong>Password</strong> for that account</li>
</ul>

<p>
Once valid credentials are entered, the Domain Controller verifies them and processes the domain join request.
</p>

<p>
<img src="images/08-AD-Adding-Users.png" alt="Credential prompt when joining the client to the domain" width="900">
</p>

<p>
This is the trust step between the workstation and Active Directory.
If the username, password, DNS settings, or network connectivity are wrong, the join will fail here.
</p>

<hr>

<h3>Step 3: Confirm the Client Successfully Joined the Domain</h3>

<p>
If the authentication is successful and the Domain Controller accepts the request, Windows displays a confirmation message:
</p>

<pre>Welcome to the mydomain.com domain.</pre>

<p>
This is an important confirmation because it tells us the client has successfully communicated with the Domain Controller and has now become a recognized member of the domain.
</p>

<p>
<img src="images/09-AD-Adding-Users.png" alt="Welcome to the mydomain.com domain message" width="900">
</p>

<p>
At this point, the client is not fully finished yet.
A restart is normally required so Windows can reload its identity and apply the domain membership correctly.
</p>

<hr>

<h3>Step 4: Verify the Client Computer Appears in Active Directory</h3>

<p>
After the client joins the domain, go back to the Domain Controller and open <strong>Active Directory Users and Computers</strong>.
Under the domain tree, open the default <strong>Computers</strong> container.
</p>

<p>
This container is where domain-joined computer objects are often placed automatically if they have not yet been moved into a separate Organizational Unit.
</p>

<p>
Here we can now see the client machine listed as:
</p>

<pre>Client-01</pre>

<p>
That object represents the workstation inside Active Directory.
This confirms the Domain Controller now knows about the machine and can manage it as a domain asset.
</p>

<p>
<img src="images/10-AD-Adding-Users.png" alt="Client-01 appearing in the Computers container in Active Directory" width="900">
</p>

<p>
This matters because once the computer object exists in Active Directory, administrators can apply policies, move the computer into OUs, and manage its access and configuration more easily.
</p>

<hr>

<h3>Step 5: Move the Client into a Dedicated Clients Organizational Unit</h3>

<p>
To keep Active Directory organized, it is best practice to separate different types of objects into their own Organizational Units, or <strong>OUs</strong>.
Instead of leaving workstations in the default <strong>Computers</strong> container, we move them into a dedicated OU.
</p>

<p>
In this lab, a new OU named <strong>_CLIENTS</strong> is used.
After moving the computer object, <strong>Client-01</strong> now appears inside that OU.
</p>

<p>
<img src="images/11-AD-Adding-Users.png" alt="Client-01 shown inside the _CLIENTS OU" width="900">
</p>

<p>
This is useful because OUs let administrators:
</p>

<ul>
  <li>Apply Group Policy to only certain machines</li>
  <li>Separate client systems from servers or admin accounts</li>
  <li>Keep the directory structure clean and easier to manage</li>
</ul>

<p>
So instead of mixing computers, users, and admins together, the domain stays structured in a way that reflects how real enterprise environments are usually organized.
</p>

<hr>

<h3>Step 6: Allow Domain Users to Access the Client Through Remote Desktop</h3>

<p>
After the client has joined the domain, the next task is to make it easier for domain users to remotely access the machine.
This is done by configuring Remote Desktop permissions.
</p>

<p>
In the <strong>Remote Desktop Users</strong> selection window, the group:
</p>

<pre>Domain Users</pre>

<p>
is added.
</p>

<p>
<img src="images/12-AD-Adding-Users.png" alt="Adding Domain Users to Remote Desktop Users on the client" width="900">
</p>

<p>
This means authenticated users from the domain are now allowed to log into the client using Remote Desktop, assuming firewall rules and connectivity are already configured properly.
</p>

<p>
This is a practical enterprise-style step because it allows users who are managed by Active Directory to sign into the workstation without needing separate local user accounts on that machine.
</p>

<hr>

<h2>
  <img src="images/13-AD-Adding-Users.png" alt="Generating domain users in Active Directory" width="40" style="vertical-align: middle; margin-right: 10px;">
  Generating Domain Users and Verifying User Logon
</h2>

<p>
This section continues the Active Directory lab by showing how a batch of regular domain users is generated, how those users appear inside the Employees organizational unit, and how one of those generated accounts can successfully sign in to the domain-joined client computer.
This is an important part of the lab because it moves Active Directory from just having the domain and administrative accounts set up to actually managing many user accounts the way a real organization would.
</p>

<p>
At this point in the environment:
</p>

<ul>
  <li>The Domain Controller is already configured</li>
  <li>The <strong>mydomain.com</strong> domain already exists</li>
  <li>The client machine has already joined the domain</li>
  <li>The client has already been placed into the proper organizational unit</li>
</ul>

<p>
Now the focus shifts to creating many normal employee user accounts and proving that one of those users can actually log on to the client machine.
</p>

<hr>

<h3>Step 1: Confirm the User Creation Script Exists and Run It</h3>

<p>
Here, the administrator is signed in as <strong>jane_admin</strong> and is working inside PowerShell.
The current directory shown is:
</p>

<pre>C:\Users\jane_admin\Documents</pre>

<p>
The <strong>ls</strong> command is used first to list the files in that folder.
This confirms that the script file <strong>create_users.ps1</strong> is present before trying to run it.
This is a good beginner habit because it verifies that the script is actually in the current directory and avoids running a command blindly.
</p>

<p>
After confirming the script exists, it is executed with:
</p>

<pre>.\create_users.ps1</pre>

<p>
The <strong>.\</strong> at the beginning tells PowerShell to run the script from the current folder.
As the script executes, PowerShell begins printing messages such as:
</p>

<pre>
Creating user: gim.sorux
Creating user: xatuw.focaco
Creating user: rebuk.qav
...
</pre>

<p>
These lines indicate that the script is automatically generating and adding multiple user accounts into Active Directory.
In a real environment, administrators often automate repetitive account creation tasks instead of manually creating each user one at a time.
This saves time, reduces mistakes, and makes it easier to create large groups of users.
</p>

<p>
<img src="images/13-AD-Adding-Users.png" alt="PowerShell running create_users.ps1 to generate domain users" width="900">
</p>

<p>
For beginners, the key takeaway here is that PowerShell is being used as an automation tool.
Instead of creating one employee at a time through the graphical interface, the script quickly creates many users in bulk.
</p>

<hr>

<h3>Step 2: Verify the New Users Appear in the _EMPLOYEES Organizational Unit</h3>

<p>
After the script runs, the next step is to verify that the accounts were actually created inside Active Directory.
This is done by opening <strong>Active Directory Users and Computers</strong> and selecting the <strong>_EMPLOYEES</strong> organizational unit.
</p>

<p>
Inside that OU, a large list of newly generated user accounts is visible.
Examples shown include usernames such as:
</p>

<pre>
bacigo.depuki
bacudo.sicur
baha.vip
bahet.wufifu
baj.vone
...
</pre>

<p>
This confirms that the PowerShell script did not just print names to the screen, but actually created real domain user accounts in Active Directory.
</p>

<p>
<img src="images/14-AD-Adding-Users.png" alt="Generated employee accounts appearing in the _EMPLOYEES OU" width="900">
</p>

<p>
This step is very important in a beginner walkthrough because verification matters just as much as execution.
If the script had errors, permission problems, or an incorrect OU path, the users might not appear where expected.
Seeing the accounts inside <strong>_EMPLOYEES</strong> proves the automation worked correctly.
</p>

<p>
It also reinforces an important Active Directory concept:
</p>

<ul>
  <li><strong>Users</strong> can be organized into OUs for structure and easier management</li>
  <li>The <strong>_EMPLOYEES</strong> OU is being used to group normal employee accounts together</li>
  <li>This makes future policy management, searching, and delegation much easier</li>
</ul>

<hr>

<h3>Step 3: Use One of the Generated Domain User Accounts to Sign In</h3>

<p>
After confirming the generated users exist in Active Directory, the next step is to prove that they are usable accounts by logging into the client machine with one of them.
</p>

<p>
In the Windows App RDP credential prompt, the user enters one of the generated domain accounts using domain format:
</p>

<pre>mydomain.com\bap.puh</pre>

<p>
This format tells Windows to authenticate the account against the <strong>mydomain.com</strong> domain rather than using a local account on the machine.
</p>

<p>
<img src="images/15-AD-Adding-Users.png" alt="RDP sign-in prompt using generated domain user bap.puh" width="900">
</p>

<p>
This is a major milestone in the lab.
It proves that:
</p>

<ul>
  <li>The user account exists</li>
  <li>The domain can authenticate that user</li>
  <li>The client machine trusts the domain</li>
  <li>The user has enough access to sign in through Remote Desktop</li>
</ul>

<p>
For beginners, this is where all the earlier setup starts coming together.
The domain join, DNS configuration, user creation, and Remote Desktop permissions all work together to allow this login to happen.
</p>

<hr>

<h3>Step 4: Watch the User's First Domain Sign-In Complete</h3>

<p>
After the credentials are accepted, Windows begins signing in as the generated user <strong>bap.puh</strong>.
The welcome screen appears while Windows prepares the profile for that account.
</p>

<p>
This first sign-in is often slower than future logins because Windows is creating the user’s local profile for the first time on that workstation.
That includes setting up the user directory, desktop profile, and other per-user settings.
</p>

<p>
<img src="images/16-AD-Adding-Users.png" alt="First successful sign-in as bap.puh on the client computer" width="900">
</p>

<p>
This is another critical proof point in the lab.
It shows the account is not just visible in Active Directory, but is actually functional as a domain user account.
</p>

<hr>

<h3>Step 5: Verify the User Reaches the Desktop Successfully</h3>

<p>
Once the logon finishes, the user reaches the Windows desktop.
The Start menu shows the currently signed-in account as <strong>bap.puh</strong>.
This confirms the user session is fully active and the sign-in completed successfully.
</p>

<p>
<img src="images/17-AD-Adding-Users.png" alt="Desktop of the generated domain user bap.puh after successful sign-in" width="900">
</p>

<p>
At this point, the lab has demonstrated that a generated employee account can:
</p>

<ul>
  <li>Exist inside Active Directory</li>
  <li>Be located in the proper OU</li>
  <li>Authenticate through the domain</li>
  <li>Log onto the client machine successfully</li>
</ul>

<p>
That means the environment is now behaving much more like a real enterprise Windows domain where multiple users can be managed centrally and sign in using their domain credentials.
</p>

<hr>


