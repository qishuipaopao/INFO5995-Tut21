Task 2 - Understand the application and build a simple model 
Application overview 
This application allows users to create accounts and log in with their username and password. When registering, the user's credentials will be stored in a local file of the device. When the user logs in, the application will compare the input information with the stored data. If the login is successful, the application will generate a session token and store it in SharedPreferences. Users can then access the profile page, and the stored session token will be deleted when logging out. 

System model 
The application mainly consists of three parts: user interface, local storage and internal logic. Users interact with applications through Activities such as MainActivity, Login and Profile. User credentials are stored in the local file (credentials.txt), while the session token is stored in SharedPreferences. The overall data flow is very simple. First of all, the user registers or logs in through the interface. Then, the application reads or writes the data in the local storage. After successful login, a session token will be generated and stored. This token is used to allow access to the profile page.
The simplified version of the system process is as follows: User → Register/Login → credentials.txt → Generate Session Token → SharedPreferences → Profile

Hypothesis and Attacker Model
We assume that the attacker can It is enough to access the application code through reverse engineering (such as decompiling APK). The attacker can also observe when the user logs in and roughly determine the generation time of the session token. The attacker's goal is to obtain or copy a valid session token to access user accounts without authorization. This means that the attacker's main concern is to bypass authentication, rather than directly accessing the stored credentials.

<img width="415" height="522" alt="image" src="https://github.com/user-attachments/assets/f2661c9d-13be-4531-af24-cd7855fb293f" />
