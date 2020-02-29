## User API Docs
```
https://api.torn.com/user/user_id?selections=fields_you_want_to_call&key=
```
***Paste  your API key at end***



- Replace **user_id** with the User ID of the player you want to get info about.

- Replace **fields_you_want_to_call** with the selection fields that you want to call. Yes, you can multiple fields for same user in a single call, but you can call more than one users in one call.

**Notes:**

1.  If you make the User API call without entering any User Id in the URL, then it will return information about your account according to the entered selection fields. For example: If you make a call to
```
https://api.torn.com/user/?selections=fields_you_want_to_call&key=
```
It will take your user ID as default and return your account information.

2. Similarly to default User Id there is a default selections field. If you make a call to  
```
https://api.torn.com/user/user_id?selections=&key=
```
There we didn't select any particular selection field, so by default it will return the data as in **profile** call. More info about profile call.

3. You can pass **from** and **to** as parameters in the URL, by entering **UNIX** timestamps of the time you want to get data about. For example:
```
https://api.torn.com/user/?selections=attacks&from=Timestamp1&key=
```
```
https://api.torn.com/user/?selections=attacks&from=Timestamp1&to=Timestamp2&key=
```
Replace **Timestamp1**  and **Timestamp2** with the Unix Timestamps.

Currently only **attacks**,  **attacksfull** , **revives**, **revivesfull**, **events**, **receivedevents** and **message** call in **User** class supports **from** and  **to** parameters.


# Reference
- [profile](#profile)
- networth
-  bazaar
-  display
-  inventory
-  hof
-  travel
-  events
-  receivedevents
-  messages
-  education
-  medals
-  honors
-  notifications
-  personalstats
-  workstats
-  crimes
-  icons
-  cooldowns
-  money
-  perks
-  battlestats
-  bars
-  basic
-  attacks
-  attacksfull
-  revives
-  revivesfull
-  stocks
-  properties
-  jobpoints
-  merits
-  refills
-  weaponexp
-  ammo
-  discord
-  gym
-  timestamp


## profile

This field returns information about ***Rank***, ***Level***, ***Life***, ***Hospital and jail time***, ***current status***, ***faction and company info***, ***icons*** etc of a user

```
https://api.torn.com/user/1?selections=profile&key=
```
It will return JSON data that looks like 

