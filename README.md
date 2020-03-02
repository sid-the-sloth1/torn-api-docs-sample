# Torn API

API is short for **Application Programming Interface**. Torn's API let's you create your custom tools for enhancing your gaming experience. Every user receive a unique API key, which can be found by going to [Preferences page](https://www.torn.com/preferences.php)  **> API Key.** 

You can make a maximum of 100 API calls per minute to the server, trying to exceed that will get your key banned.

 **In order to deal with the excess load put on Torn Server due to API, caching has been put in place. If you make same API call more often than every 30 seconds, it will return the data as it returned in previous call. So it is a good idea, to wait for 30-35 seconds before making the same request again.** 

## Basics
- [Errors](#errors)
- [Classes](#classes)


### Errors
 **Error Code** 0 => 'Unknown error' : Unhandled error, should not occur.

 **Error Code** 1 => 'Key is empty' : Private key is empty in current request.

 **Error Code** 2 => 'Incorrect Key' : Private key is wrong/incorrect format.

 **Error Code** 3 => 'Wrong type' : Requesting an incorrect basic type.

 **Error Code** 4 => 'Wrong fields' : Requesting incorrect selection fields.

 **Error Code** 5 => 'Too many requests' : Current private key is banned for a small period of time because of too many requests  **(max 100 per minute).** 

 **Error Code** 6 => 'Incorrect ID' : Wrong ID value.

 **Error Code** 7 => 'Incorrect ID-entity relation' : A requested selection is private  **(For example, personal data of another user / faction).** 

 **Error Code** 8 => 'IP block' : Current IP is banned for a small period of time because of abuse.

 **Error Code** 9 => 'API disabled' : Api system is currently disabled.

 **Error Code** 10 => 'Key owner is in federal jail' : Current key can't be used because owner is in federal jail.

 **Error Code** 11 => 'Key change error: You can only change your API key once every 60 seconds'.

 **Error Code** 12 => 'Key read error: Error reading key from Database'.



### Classes
 Class means objects having same type of properties.Torn API has 6 classes of API requests. These classes are:

- [User](#user): To request data related to a user's profile.

- [Properties](#properties): To request data about properties.

- [Faction](#faction): To request information about a faction and it's members.
- [Company](#company): To get information about a company and it's employees.
- [Item Market](#item-market): To get information about Bazaar, Item Market and Points Market.
- [Torn](#torn): To get information related to Torn as a whole. It includes ***Stocks***, Gyms, Rackets, Items etc.




### User
```
https://api.torn.com/user/user_id?selections=fields_you_want_to_call&key=
```
***Paste  your API key at end***



- Replace **user_id** with the User ID of the player you want to get info about.

- Replace **fields_you_want_to_call** with the selection fields that you want to call. Yes, you can multiple fields for same user in a single call, but you can't call more than one users in one call.

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
- [networth](#networth)
- [bazaar](#bazaar)
- [display](#display)
- [inventory](#inventory)
- [hof](#hof)
- [travel](#travel)
- [events](#events)
- [receivedevents](#receivedevents)
- [messages](#messages)
- [education](#education)
- [medals](#medals)
- [honors](#honors)
- [notifications](#notifications)
- [personalstats](#personalstats)
- [workstats](#workstats)
- [crimes](#crimes)
- [icons](#icons)
- [cooldowns](#cooldowns)
- [money](#money)
- [perks](#perks)
- [battlestats](#battlestats)
- [bars](#bars)
- [basic](#basic)
- [attacks](#attacks)
- [attacksfull](#attacksfull)
- [revives](#revives)
- [revivesfull](#revivesfull)
- [stocks](#stocks)
- [properties](#properties)
- [jobpoints](#jobpoints)
- [merits](#merits)
- [refills](#refills)
- [weaponexp](#weaponexp)
- [ammo](#ammo)
- [discord](#discord)
- [gym](#gym)
- [timestamp](#timestamp)




#### profile

This field returns information about ***Rank***, ***Level***, ***Life***, ***Hospital and jail time***, ***current status***, ***faction and company info***, ***icons*** etc of a user.

```
https://api.torn.com/user/1?selections=profile&key=
```
It will return JSON data as shown [here](sample/User_profile.json)


#### networth
This a private API call, which means that you can't request this information for another user. If you try to make **networth** API call for another user, then it will give you  **Error Code 7**.

```
https://api.torn.com/user/?selections=networth&key=
```

Calling this URL returns value of ***items, stocks, points and cash*** that you have stored in your Vault, Bank Investment, Company, Bookies, Cash on Hand, Caymans, Piggy Bank etc. 
It also returns a key named **parsetime** which according to IceBlueFire is
> Parsetime is yes, how long it took to generate it. Networth is a heavier call in the api.

A sample of the data returned from **networth** call can be found [here](sample/User_networth.json).


#### bazaar
This call can be used to get information about the items a user has in their bazaar.
```
https://api.torn.com/user/2274961?selections=bazaar&key=
```
It returns an **array of objects** containing information about the ***Items' name, quantity, market value and the price that the user has put it on for***.  Sample data returned by this call can be seen [here](sample/User_bazaar.json).


#### display

This method is used to get information about the items a user has in their Display Case.

```
https://api.torn.com/user/1615969?selections=display&key=
```
This method returns an **array of objects** containing ***Name, type, quantity, circulation and market value*** of the items a user has in their Display Case. 
Sample data returned by this call can be found [here](sample/User_display.json).



#### inventory
This is a private call, means you **cannot** request this data for another user, if you do try you will be met with **Error Code 7**.

```
https://api.torn.com/user/?selections=inventory&key=
```

Calling this method returns an **array of objects** containing information about ***Items in your inventory, their market price, quantity and whether you have them currently equipped or not.*** Sample data that is returned by calling it can be found [here](sample/User_inventory.json).


#### hof

This method is used to get your ranks in **Hall of Fame** under various categories. It is a private call, means you can't access this data for another user, If you try to do so then you will be met with **Error code 7**.

```
https://api.torn.com/user/?selections=hof&key=
```
It returns a JSON string containing your rank and value in various Hall of Fame categories. Sample data returned by this method can be found [here](sample/User_hof.json).


#### travel

This call is used to request data about your remaining travel time. This is a private call, means trying to get this data for another user will get you Error Code 7.
```
https://api.torn.com/user/?selections=travel&key=
```

Sample data returned from this method looks like this.

```
"travel": {
		"destination": "Switzerland",
		"timestamp": 1583027728,
		"departed": 158302727,
		"time_left": 7294
	}
}
```
 **timestamp** represents the instant when you will reach your destination and  **time_left** tells how many seconds away from your destination you are.

#### events

This call lets you access your events. It shows last 100 events(maybe less if you are using ```from``` and ```to``` parameters. This is a private call and trying to access this information for other user will get you **Error Code 7**.

```
https://api.torn.com/user/?selections=events&key=
```

This call supports ```from``` and ``` to``` parameters.


#### receivedevents

This is a fairly new method added into the API. It let's you access the events that you have received from other players. This is a private call and trying to access this information for other user will get you **Error Code 7**.

```
https://api.torn.com/user/?selections=receivedevents&key=
```

This call supports ```from``` and ``` to``` parameters.


#### messages

This method is used to request the mails received by you. Again, it's a private call and you can't access this data for another user, but if you do try to call other user's message then you will get  **Error Code 7.** 
```
https://api.torn.com/user/?selections=messages&key=
```


#### education

This method returns information about the education course that you are currently taking and the courses that you have already finished.

```
https://api.torn.com/user/?selections=education&key=
```
It returns data that looks like this:
```
{
  "education_current": 39,
  "education_timeleft": 990,
  "education_completed": [
    1,
    2,
    3,
    4,
    5,
    6
  ]
}
```
 **education_current** represents the code of current education course you are taking.
 **education_timeleft** represents the time remaining for the current education course you are taking (in seconds).

 **education_completed** returns an  **array** including the code of the education courses you have already finished.

#### medals

This call returns information about **medals you have received**. It is a private call and trying to get this information for another user will get Error Code 7.

```
https://api.torn.com/user/?selections=medals&key=
```
The call returns data that looks like:
```
{
  "medals_awarded": [
    1,
    2,
    3,
    4,
    5
  ],
  "medals_time": [
    1555292998,
    1540708126,
    1530367856,
    1530230510,
    1531961560
  ]
}
```

 **medals_awarded** represents an array of the code of medals that you have received and  **medals_time** shows the Epoch Timestamp of when you received the medal, in the same order.

#### honors

This call us used to get information about "Honors" received by a user. Just like the [medals](#medals) call it is also a private call and you can not request this data for another user.

```
https://api.torn.com/user/?selections=honors&key=
```
It returns data that looks like:
```
{
  "honors_awarded": [
    1,
    2,
    3,
    4,
    5
  ],
  "honors_time": [
    1555292998,
    1540708126,
    1530367856,
    1530230510,
    1531961560
  ]
}
```


 **honors_awarded** represents an **array** containing the codes of  **honors** that you have received. 

And the element at the same index in **honors_time** array represents the Epoch Timestamp of the instant when user received the honor.





