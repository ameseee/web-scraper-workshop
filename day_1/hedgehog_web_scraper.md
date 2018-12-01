# Hedgehog Web Scraper

## Set Up

### Front End
- Go to [this link](https://github.com/ameseee/hedgehog-fe)
- Click "Fork" in the top right corner. This will create a copy of the project, but in your GitHub account. Once it's done, you should see a page with "your-username/hedgehog-fe" in the top left corner.
- Click the "Settings" button. Scroll down until you see "GitHub Pages". In the dropdown menu that currently says "None", select "Master Branch" (the first one). Then, click "Save".
- Scroll back down to the GitHub Pages section. You should now see a blue section above that dropdown that says something like, "✅ Your site is published at https://ameseee.github.io/hedgehog-fe/". Open that link in another tab. It may take a while to load, but it can work on that while we work on other things. We will come back to it later today - this is our production version of the app, and will not change as we go. Click and drag that tab, it will go into it's own window. Minimize that window. This will help us not get confused between our development version and production version.
- Open up GitHub Desktop (by typing in "GitHub" into the computer's search bar on the bottom left, then clicking on "GitHub Desktop").
- Click the button on the right side of the page that says "Clone a Repository".
- A list of all your repositories attached to your GitHub account will appear. Click on "hedgehog-fe", then click the blue "Clone" button. This will create a copy of that project on your computer.
- In GitHub Desktop, you'll see hedgehog-fe on the left. Double-click it to enter the project.
- Now, open the Command Prompt program (by typing in "Command" into the computer's search bar on the bottom left, then clicking on "Command Prompt"). To navigate to the folder where our project is, type `cd Documents/GitHub/hedgehog-fe`. Press enter.
- Type `start index.html`. Press enter. This will create a development version of our app, where we can see each change as we go.
- Your browser will open to a page that looks something like this:
![inline](../assets/start_view_screenshot.png)
- Close the command prompt.

### Web Scraper
- Go to [this link](https://github.com/ameseee/hedgehog-scraper)
- Click "Fork" in the top right corner. This will create a copy of the project, but in your GitHub account.
- In GitHub Desktop, click "Current Repository" in the top left. The click the small "Add" dropdown. Select "Clone repository..."
- A list of all your repositories attached to your GitHub account will appear. Click on "hedgehog-scraper", then click the blue "Clone" button. This will create a copy of that project on your computer.
- In GitHub Desktop, you'll see hedgehog-scraper in a list on the left. Double-click it to enter the project.
- Select "Repositories", the select "Open in Atom".
- Open a new command prompt by starting to type in "command prompt" into the bottom left search bar of your screen, then press "enter".
- Type `cd Documents/GitHub/hedgehog-scraper`. Press enter.
- Type `npm install`. Press enter.
- Type `node server.js`. Press enter.
- You should see something like this in your command prompt:
```bash
  app running on 3000
```
- Open a new tab in the browser. Go to `http://localhost:3000/`. You should see a very small "Hedgehog Time" in the top left corner of the screen. It may take some time to load. You are ready to go!
- Keep your command prompt open at all times!

## See The Finished Product

Let's take a quick break from our computers to see the final product!

## Write Your First Endpoint

What is an endpoint?
> An endpoint is a location where specific information can be accessed. It is set up in the back end of an application.

In `server.js`, we already have one endpoint written on lines 12-14. It is very simple - it says that when we visit the root of the page in the browser, we will see "Hedgehog Time". Try changing the words inside the quotes to something else. Now, refresh the page in the browser and you should see the words you typed in!

Let's write an endpoint of our own to get a little more practice. Starting on line 17, below the comment that says:
```js
// your endpoint
```
let's follow a similar pattern as we saw above. Add the following code in (but make the sentence your own!):

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
    var nightmare = Nightmare({ show: true });

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

## The Final Step - Connect to our Front End

Go back to the tab in your browser that looks something like: `https://<your username>.github.io/hedgehog-fe/`. Type in a celebration, and see what happens.

At this point, you should see the little browser come up, the bot do it's thing, then the images show up in your browser. If that didn't work out, go back to the browser tab that you originally opened by typing `open index.html` in your terminal - it looks something like: `file:///Users/<username>/personal_projects/hedgehog-fe/index.html`. Try the same thing. Does the little browser open up? Do new images come up a few seconds later?

If you still don't have new images oh hedgehogs, find an instructor and we will help you hunt down the problem. You are so close!

Now that we are done, we don't need that little browser to pop up and show what the bot is doing every time. In your scraper endpoint, you currently have a line of code that looks like:

```js
    var nightmare = Nightmare({ show: true });
```

Let's remove the `{ show: true }` so we just have `var nightmare = Nightmare()`. Run the program in your browser again to make sure it is still working as you want it to.
