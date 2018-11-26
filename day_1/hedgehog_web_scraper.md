# Hedgehog Web Scraper

## Set Up

### Front End
- Go to [this link](https://github.com/ameseee/hedgehog-fe)
- Click "Fork" in the top right corner. This will create a copy of the project, but in your GitHub account.
- In your project, click the green "Clone or Download" button. Then, click the clipboard icon.
- Now, go into your terminal. Type `git clone `  and "control v". You should see something like: `git clone https://github.com/<your username>/hedgehog-fe.git`. Press enter.
- Type `cd hedgehog-fe`
- Type `open index.html`
- Your browser will open to a page that looks something like this:
![inline](../assets/start_view_screenshot.png)
- Keep your terminal open at all times!

### Web Scraper
- Go to [this link](https://github.com/<your username>/hedgehog-scraper)
- Click "Fork" in the top right corner. This will create a copy of the project, but in your GitHub account.
- In your project, click the green "Clone or Download" button. Then, click the clipboard icon.
- Back in your terminal, type "control", "alt", and "t" at the same time. A new window should open.
- Type `cd ..`. In this new window, follow this next set of directions.
- Now, go into your terminal. Type `git clone ` and "control v". You should see something like: `git clone https://github.com/<your username>/hedgehog-scraper.git`. Press enter.
- Type `cd hedgehog-scraper`
- Type `npm install`
- Type `npm start`
- You should see something like this in your terminal:
```bash
  > a-hedgie-scraper@1.0.0 start /Users/amyholt/personal_projects/a-hedgie-scraper
  > node server.js

  app running on 3000
```
- Open a new window in the browser. Go to `http://localhost:3000/`. You should see a very small "Hedgehog Time" in the top left corner of the screen. You are ready to go!
- Keep your terminal open at all times!

## Dev Tools Warm Up

Go to the tab in your browser where you can see the hedgehogs with a purple background.

Open your developer tools (right click, click inspect). You can click the three-dot icon in the top right corner to rearrange where the dev tools appear on your screen.

Click the little arrow in the top left corner of the dev tools. Now, hover over the title of the app. Do you notice how different parts of the page highlight as you move the mouse over them? If you click on the title of the page, you will see the HTML that created it, in the elements panel!

Work with your partner to answer the following questions. This activity will help you use the dev tools so that you can scrape later today!
- What HTML element is the title in?
- What is the "id" of the hedgehog that has marshmallows in his spikes?
- What is the "src" of the hedgehog that is cuddling in front of the ocean?
- What is the "id" of the input where users type in their keyword?
- What is the "type" of the input/button where users click to get hedgie photos?

## Write Your First Endpoint

What is an endpoint?
> explain

As you can see, we already have one endpoint written on lines 12-14. It is very simple - it says that when we visit the root of the page, we will see "Hedgehog Time". Try changing the words inside the quotes to something else. Now, refresh the page in the browser and you should see the words you typed in!

Let's write an endpoint of our own to get a little more practice. Starting on line 17, below the comment that says:
```js
// your endpoint
```
let's follow a similar pattern as we saw above. Add the following code in (make the sentence your own!):

```js
app.get('/pets', (req, res) => {
  res.send("insert a sentence about your favorite pet here!");
});
```

Now, refresh the browser. Nothing has changed, has it? Well, our endpoint has, but the computer can't read our mind and know what we are looking for. In the url bar, we actually need to visit `http://localhost:3000/pets`. Now do you see your sentence? If you don't, please let an instructor know and we will help you out.

Let's take it one step farther - we are going to give the endpoint information and expect it to be "smart". Below your pets endpoint, let's add another:

```js
app.get('/:name', (req, res) => {
  var name = req.params.name;

  res.send(`Hi, ${name}!`);
});
```

Now, go back to the browser and visit `http://localhost:3000/<your name>` - mine would look like: `http://localhost:3000/amy`. What happens? Talk with your partner and try to figure out why this may be happening. It's ok if you aren't sure, we will discuss it as a group.

## Write Your Hedgehog Endpoint

Now that we are starting to understand how endpoints work, we are going to start writing one for a Hedgehog Web Scraper. It may not make complete sense the first time we go through this, but we will have plenty of practice!

First, let's start by adding the following code to our file:

```js
// scraper endpoint

app.get('/hedgie/:keyword', (req, res) => {
  var keyword = req.params.keyword;

});
```

In the code above, we have created an endpoint for `http://localhost:3000/hedgie/:keyword`. The "keyword" can be anything the user types in there. Then, on the next line we create a variable that stores that keyword that was typed in. We aren't returning anything yet, so if you go to this endpoint in your browser, you shouldn't see anything. Not yet.

Now, inside of this endpoint we need to write our web scraper function. Let's call it `findHedgieImage` and it will take an argument of the `keyword`. Update your code to look like this:

```js
app.get('/hedgie/:keyword', (req, res) => {
  var keyword = req.params.keyword;

  function findHedgieImage(keyword) {

  }

});
```

## Time To Scrape

Now is where the real work begins. We talked about `nightmare` earlier. It is a tool that allows us to scrape the web. To use it, we first to tell our function about it by creating what is called an instance. Let's add this into the function:

```js
  function findHedgieImage(keyword) {
    var nightmare = Nightmare();

  }
```

Now that the function knows about `nightmare`, we need to use it! We can give `nightmare` all kinds of directions for the things a human would do to go through a website. Visit `https://github.com/segmentio/nightmare#interact-with-the-page` and read through - you'll see `goto`, `click`, and more.

Now that we are getting a feel for what we can do with `nightmare`, let's tell it to go to google.

```js
  function findHedgieImage(keyword) {
    var nightmare = Nightmare();

    return nightmare
      .goto('https://www.google.com')
  }
```

Cool, we are at `google.com` - what do you want to tell the bot to do next? Let's work through this with our partners.

### Partner Google

* **Partner with longer hair:** You are the note taker. Keep track of each button click you partner makes, each thing they type, etc.
* **Partner with shorter hair:** If you start at `google.com` and you want to find "hedgehog halloween" images, what would you do? Go through those steps (slowly so your partner can take note). Make sure you tell your partner each little thing you do.

We will discuss this as a group once everyone has had time to complete this activity.

Now that we know all the steps we would take, we need to tell our bot. At `google.com` we need to insert some text into the input field. How do we communicate with the computer about where we want our text inserted? Let's use our Developer Tools!

### Dev Tools

Go back to your browser. If the developer tools are not yet open, open them. Make sure you are in the elements panel. Click that little arrow in the top left corner, then hover over the input field where you would type your search term. When it is highlighted, click it. What information do you see in the elements panel? It has a title of "Search"! Let's tell `nightmare` to input some text wherever it sees 'input[title="Search"]', then tell it what to input.

```js
  function findHedgieImage(keyword) {
    var nightmare = Nightmare();

    return nightmare
      .goto('https://www.google.com')
      .insert('input[title="Search"]', `hedgehog ${keyword}`)
  }
```

How did we insert? The first thing we told this method is **where** to insert something. Second, we told it **what** to insert. In this case, we know we always want to search for hedgehogs, but the second word will vary. Our variable `keyword` helps us out here!

Now, we need to click the "Google Search" button. Use your dev tools to find that input value. Then, look at the code below and see if you were right!

```js
  function findHedgieImage(keyword) {
    var nightmare = Nightmare();

    return nightmare
      .goto('https://www.google.com')
      .insert('input[title="Search"]', `hedgehog ${keyword}`)
      .click('input[value="Google Search"]')
  }
```

Now that we have typed in our text and clicked the button, we need to tell the bot to wait until the next page loads before it tries to do something else. Under your `.click` method, add in the following line of code:

```js
  .wait('a.q.qs')
```

This line is saying "wait until you see an `a` tag with the classes `q` and `qs` (which is the "Images" button) until you do the next thing, please".

Now that it's there, let's click on it:

```js
  .click('a.q.qs')
```

Now, we need to find a `<div>` with the classes of `res` and `med`. It is the `div` that is outside of all the search results (below ads, if there are any). Go to google.com, type in a search term, click search, then on the page you are brought to, and look for this `<div>` using your Dev Tools. After clicking 'a.q.qs', we want to make sure this `<div>` exists. After your `.click` method, we need to wait on 'div#res.med'. Update your code:

```js
 return nightmare
      .goto('https://www.google.com')
      .insert('input[title="Search"]', `hedgehog ${keyword}`)
      .click('input[value="Google Search"]')
      .wait('a.q.qs')
      .click('a.q.qs')
      .wait('div#res.med')
```

Once the `.wait('div#res.med')` function completes, it's finally time to DO something with the information we're navigating to! We will use the `.evaluate` method. Inside of it, we will select all of the divs that are around the photos. They are in a list, but the _kind_ of list we need. The line that starts with `var list = ` changes our list into an `array`. After that, we `map` over the array of photos, and return each `src` which is the URL link for the photo. Update your code with this:

```js
      .wait('div#res.med') // you should already have this line
      .evaluate(function() {
        var photoDivs = document.querySelectorAll('img.rg_ic');
        var list = [].slice.call(photoDivs);

        return list.map(function(div) {
          return div.src;
        });
      })
```
Now, we need to tell `nightmare` that we are finished scraping the web. On the line below your closing `.evaluate` method, add in:

```js
      .end()
```

## Finished Scraping 🎉 Finish Endpoint

Great work! The thing is, we have not _done_ anything with our data. We need to complete the endpoint by sending this data. We are going to use a couple `.then` methods. `.then` just waits for the method before it to complete, then does whatever you tell it to! On the line below your `.end()`, add in the following code:

```js
      .then(function (result) {
        return result.slice(1, 5);
      })
```

This line of code takes our (very long list) and trims it down to the first four photos. Our HTML is currently set up to display 4, but if we modified that, we could show as many as we want!

We still have not send data for this endpoint. After the first `.then`, add in:

```js
      .then(function (images) {
        res.json(images);
      })
```

Finally, we have sent the image URLs off in the endpoint response!

One thing - what if something goes wrong? How will we know? We can use a method called `.catch`. Add in the following code below your last `.then` method:

```js
      .catch(function (error) {
        console.error('Search failed:', error);
      });
```

This will print an error to the console if something goes wrong.

The very last thing we need to do is _call_ this function, so it actually starts scraping the web. This happens at the very bottom of the endpoint. Your endpoint should look like this:

```js
app.get('/hedgie/:keyword', (req, res) => {
  var keyword = req.params.keyword;

  function findHedgieImage(keyword) {
    var nightmare = Nightmare({ show: true });

    return nightmare
      .goto('https://www.google.com')
      .insert('input[title="Search"]', `hedgehog ${keyword}`)
      .click('input[value="Google Search"]')
      .wait('a.q.qs')
      .click('a.q.qs')
      .wait('div#res.med')
      .evaluate(function() {
        var photoDivs = document.querySelectorAll('img.rg_ic');
        var list = [].slice.call(photoDivs);

        return list.map(function(div) {
          return div.src;
        });
      })
      .end()
      .then(function (result) {
        return result.slice(1, 5);
      })
      .then(function (images) {
        res.json(images);
      })
      .catch(function (error) {
        console.error('Search failed:', error);
      });
  }

  findHedgieImage(keyword);

});
```

It's official, we should have hedgehogs. In your browser, visit `http://localhost:3000/hedgie/<insert a word>`. You should see another little browser pop up - your bot is working away! Once it is done, you should see a list of 4 URLs to photos of hedgehogs with your keyword. Not actual photos _yet_, but soon we will see it all come together.
