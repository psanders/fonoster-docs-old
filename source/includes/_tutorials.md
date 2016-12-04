# Tutorials

## Survey Tutorial

> <h3 class='toc-ignore'>Full Code</h3>

```javascript
var candidates = {
  "1": "{name:'Donald Trump'}",
  "2": "{name:'Hillary Clinton'}",
  "3": "{name:'Benny Sanders'}"
};

// Force hangup after two minutes
hangup(120);
voice('lisa');

say('Hello, this is a presidential poll from the Georgia Statistics Center.');

var keyPressed = gather(say('If you would like to be remove from our list, press 7'), {timeout: 10, numDigits: 1});

if (keyPressed == 7) {
    http.post('https://georgia.gov/removeFromList')
    .timeout(5000)
    .basicAuth("username", "password")
    .then(function(result) {
        if (result.body == 'OK') {
            say('You have been remove from our list');
        } else {
          // Do nothing
        }
     });
}

// Configure the behavior of _gather_
var config = {
    finishOnKey: '*',
    timeout: 1,
    numDigits: 1
};

while(true) {
    var keyPressed = gather(say('For Trump Press one. For Hillary, press two and for Sanders 3'), config);
    
    if (keyPressed != '1' && keyPressed != 2 && keyPressed != 3) {
	say('I could not register your selection. Lets try again.');
        continue;
    }

    // Store with call record
    stash('candidate', keyPressed);
    say('You selected option ' + keyPressed + ', ' + candidates[keyPressed].name);
    break;
}

say('Thanks for participating in this poll. To review the results, go to www.georgia.gov. Goodbye!');
```

This tutorial shows how to write a survey with Javascript and the RESTful API. The requirements are as follows:

* The application must present a list of few political candidates
* Must provide an option to remove the user from the call-list
* An English voice must be used
* The call will last no more than 2 minutes
* The customer keyPressed must be saved

Let's start by creating the list of candidates

Next, let's tell our app that it must hang up once two minutes have elapsed. We will also use _voice('lisa')_ to set Lisa (a female English voice) as the default voice (For more voices, check out the *Say* verb documentation). 

Let's now use the verb *Gather* to ask the customer if it wants to get off the call-list. Remember, that the _Gather_ verb must be used in combination with _Wait_, _Say_ or _Play_.

The final step is to ask the customer for the candidate of choice and _Stash_ the result with the call-record.

