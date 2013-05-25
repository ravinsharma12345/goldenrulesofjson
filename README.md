The Golden Rules of JSON
========================

Are you writing a JSON API? Here's the Golden Rules of JSON to adhere to. 

Do you have a rule that isn't mentioned here? Make a pull request or [email me](brad@bradleycurran.com). 

Rule #1 - A Computer Reads the JSON Data
----------------------------------------

Above all, remember that your JSON API is used as a way to expose information to a client. The direct client is a computer, not a person. 

Computers don't care about how nicely the whitespace has formatted the response or that you've made a key into the data to save a couple of characters. 

What computers (and the developers behind them) want is a consistent and reliable interface that follows basic guidelines and best practices for JSON. 

If you really want to save bandwidth, remove all formatting whitespace and gzip your responses. It's as easy as that. 

Rule #2 - Use Static Keys
-------------------------

Sometimes people think they can be smart and set the keys of data as the data itself. While it makes it less easier to read for humans, computers find this a little more difficult to parse. 

### Instead of This ###

	{
	  "Dogs": [],
	  "Cats": [],
	  "Rabbits": []
	}

### Do This ###

	{
	  "animals": [
	    {
	      "name": "Dogs",
	      "items": []
	    },
	    {
	      "name": "Cats",
	      "items": []
	    },
	    {
	      "name": "Rabbits",
	      "items": []
	    }
	  ]
	}

By writing your API with static keys, the client code should be able to parse your results automatically using a library like Gson. 

Rule #3 - Keep One Type of Object In Each Array
-----------------------------------------------

In an effort to make JSON data more readable, API developers sometimes put more than one type of object in a single array. 

### Instead of This ###

    {
      "items": [
        {
          "type": "store",
          "storename": "The Pet Barn",
          "employees": 8
        },
        {
          "type": "animal",
          "name": "Rufus",
          "breed": "Dalmation"
        },
        {
          "type": "animal",
          "name": "Molly",
          "breed": "Turtle"
        }
      ]
    }

### Do This ###

	{
	  "stores": [
	    {
	      "name": "The Pet Barn",
	      "employees": 8
	    }
	  ],
	  "animals": [
	    {
	      "name": "Rufus",
	      "breed": "Dalmation"
	    },
	    {
	      "name": "Molly",
	      "breed": "Turtle"
	    }
	  ]
	}

This way, clients can tell the structure of the array without having to manually check the "type" value. If you're using something like a "type" key, it's generally a bad smell. 
