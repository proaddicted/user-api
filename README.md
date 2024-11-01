Laravel Version - 8.X
PHP Version to Run Project -  7.4.x 
Packages Used - 
			1.Guzzle Http Client For API Call


For Easy to user API in Whole Project we can put the API Link (https://randomuser.me/api/) and Per Call Fetch in env file.

NO_USERS_PER_CALL = 5 
FETCH_USER_API = 'https://randomuser.me/api/'

Project Code Explanation-



Part 1 User Creation & Task Schedule

1.First we have created a command which should create users (php artisan make:command CreateUsers) . A file been created in app/Console/Commands folder in this file we will put the logic of creating users by scheduling task.

2.Give a Signature in the CreateUsers Command.

3.Make Migration for Tables With Models

User Details Table: Store user's gender

Location Table: Store user's city and country information

php artisan make:model UserDetail -m

php artisan make:model UserLocation -m


4.Run Migration

5.Write Logic in Command and Schedule It in Kernel.php in Console Folder and Then Write Code  $schedule->command('create:user')->everyFiveMinutes(); and Then Run php artisan schedule:run it will run the create:user command in each 5 minutes



Part 2 Public API Create

1.Create A Controller by following Command php artisan make:controller UserController

2.Create a function named index and put the logic in it as needed 

3. Put the functions route in app/routes/api.php (Without authentication middleware)

4.Run php artisan serve and test the API in POSTMAN or Other API Checking Platforms -  API Will Be Like 
	http://127.0.0.1:8000/api/users?limit=10&gender=male&country=Netherlands



5. Test Cases

	1. With gender and country  filter
		http://127.0.0.1:8000/api/users?limit=10&gender=male&country=Netherlands

		Response: 
				"data": [
        {
            "name": "Mr Badr Bulthuis",
            "email": "badr.bulthuis@example.com",
            "gender": "male",
            "country": "Netherlands",
            "city": "Austerlitz"
        },
        {
            "name": "Mr Urvin Nikkels",
            "email": "urvin.nikkels@example.com",
            "gender": "male",
            "country": "Netherlands",
            "city": "Koudum"
        }
    ]
 
	2. With Column Selector
		http://127.0.0.1:8000/api/users?limit=10&gender=male&country=Netherlands&column_select=users.name,user_details.gender
		Response: 
				"data": [
        {
            "name": "Mr Badr Bulthuis",
            "gender": "male"
        },
        {
            "name": "Mr Urvin Nikkels",
            "gender": "male"
        }
    ]
