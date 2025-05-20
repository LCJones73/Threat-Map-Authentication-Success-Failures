# Threat-Map-Authentication-Success-Failures
A comparison between the Successful Login Map from the Deep Dive creation project with a similar map showing "Failed Logins".<BR><BR>

> [!note]
> To better understand this section, consider reviewing the [Threat Maps Creation (Deep Dive)](https://github.com/LCJones73/Threat-Maps-Creating-Deep-Dive) first.<BR><BR>

In the "Threat Maps Creating Deep Dive we saw the Successful Login Threat Map:<BR><BR>
![Step 12 Threat Map](https://github.com/user-attachments/assets/11864d80-bdab-4257-91da-54a150a485f0)<BR><BR>

We used the following KQL code to search for Successful Logins and generate the map above:<BR><BR>

![image](https://github.com/user-attachments/assets/b3667978-650b-44ee-9dbd-f8f0420c1e53)

If you look at the code, you will see in Line 5 the following code: _| where ResultType == 0\n|_ - take note of this as we compare the new code.<BR><BR>

The following code will be used to search and find "Failed Logins":

![image](https://github.com/user-attachments/assets/e2d4028c-8677-4aa5-b685-06efb945bfa6)<BR><BR>

Which generates the following Threat Map:<BR><BR>

![image](https://github.com/user-attachments/assets/8f0704a3-aaea-4336-b9f3-d24d9a9aeeee)

When inspecting this code, you will see the change on line 5 goes from _| where ResultType == 0\n|_ to the following _| where ResultType != 0\n|_ <BR><BR>

> [!IMPORTANT]
> Let's Break This KQL Code Down!<BR><BR>
> The "_| where ResultType != 0\n|_" code filters the SigninLogs table to include only records where the ResultType is not equal to 0. According to Microsoft's documentation, a ResultType of 0 indicates a successful sign-in, while any other value signifies a failure. <BR><BR>
> By applying this filter, the query focuses on failed login attempts. Subsequent lines in the query summarize these failed attempts by user identity and geographical location, which can be useful for detecting patterns or anomalies in sign-in failures.<BR><BR>
> Alternatively, the "_| where ResultType == 0\n|_" code is designed to filter the SigninLogs table to retrieve records where the ResultType equals 0. In the context of Microsoft Entra ID (formerly Azure Active Directory), a ResultType of 0 indicates a successful sign-in attempt. This is corroborated by Microsoft's documentation, which states that ResultType provides the result of the sign-in operation, with 0 representing success and other values indicating specific failure reasons.<BR><BR>
> By applying this filter, the query focuses exclusively on successful login events. This can be particularly useful for analyzing user behavior, monitoring access patterns, or auditing successful authentications within your organization.<BR><BR>
These are simple chunks we are examining in the Kusto Query Language (KQL) to better understand how it works. In this case we are creating Failed and Successful Login Maps. Next we will create a map showing users who are creating resources like VMs inside a Microsoft Azure tenent.
