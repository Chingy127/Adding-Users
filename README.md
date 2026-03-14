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

