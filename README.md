# Film Finder

## You’ve caught up on your list of TV shows and movies and want to get recommendations for what to watch next, but aren’t sure where to look. You’ll be able to choose from several genres, and like or dislike a movie to get another suggestion.

In this project, you’ll use your knowledge of HTTP requests and asynchronous JavaScript to create a movie discovery app that will recommend random movies by genre.

### Before you begin, you’ll need to [create an account](https://www.themoviedb.org/signup) on The Movie Database website.

# Populate Drop-down Menu with Genres
## Instructions

- Save the API key you obtained from the TMDB API to the tmdbKey variable. We’ll be making multiple calls to the TMDB API and will reference this key in the upcoming steps.
- Check the TMDB documentation to find the API’s base URL, and save it to the tmdbBaseUrl variable.
  We will append specific endpoints to this URL for each of our requests to the TMDB API.
- Check the TMDB documentation to find the “Genres” API endpoint. Create a variable called genreRequestEndpoint inside `getGenres()` and set it to the “Genres” API endpoint.
- We will use query parameters to add more specificity to our request. Still inside the getGenres() function, create a variable called requestParams and set it to a query string where the key is api_key and the value is tmdbKey.
  Query strings start out with a question mark, ?, followed by the key/value pairs. The format looks like this:

  ```
  const queryString = `?key=value`;
  ```

- Let’s put together the URL where we’ll send our fetch request. Create a variable called urlToFetch and set it to a string that consists of tmdbBaseUrl, followed by genreRequestEndpoint, followed by requestParams.
- Turn `getGenres()` into an asynchronous function that returns a promise. We’ll include our `fetch()` request in this function, and making it asynchronous will simplify handling the promise our API call returns.
- Inside the `if` statement of our `try` block, we’ll capture the data that we need to populate our dropdown menu. To get the requested data, convert the `response` object to a JSON object. Await the resolution of this method and save it to a variable called `jsonResponse`.
- To make sure your code is working, log `jsonResponse` to the console inside our if statement. You should see a single object with a single key, `genres`. The value of genres is an array that lists TMDB’s genres.
  Save the `genres` property of `jsonResponse` in a variable called `genres`. Log this variable to the console to confirm that it contains the correct information.
- Return genres as the very last line of the if statement inside our try block of the `getGenres()` function.

# Get a Random Movie
## Instructions

- For the next several steps we’ll be working inside `getMovies()` to fetch a list of movies based on the genre selected from the list of genres we returned in `getGenres()`.

  Check the [TMDB documentation](https://developers.themoviedb.org/3/discover/movie-discover) to find the “Movie Discover” API endpoint. Below the selectedGenre variable declaration, save this endpoint to a variable called `discoverMovieEndpoint`.

- Like we did for `getGenres()`, we’ll create a variable called `requestParams`. Set it equal to a query string with two parameters. The first will be our `api_key` with the value, `tmdbKey`. The second parameter will have the `with_genres` key with its value set to the `selectedGenre` variable.

  A query string starts with a question mark, `?`, and each key/value pair is separated by the `&` symbol.

  ```
  const queryString = `?keyOne=valueOne&keyTwo=valueTwo`;
  ```

  `selectedGenre` stores the returned value from a helper function (the `getSelectedGenre()` function in helpers.js) that captures the user’s selected genre.

  Let’s also put together the URL where we’ll send our fetch request. Create a variable called `urlToFetch`. Set it to a string that consists of `tmdbBaseUrl`, followed by `discoverMovieEndpoint`, then `requestParams`.

- Turn `getMovies()` into an asynchronous function that returns a promise. This will simplify handling the promise that our `fetch()` request will return.

  Add try/catch blocks inside `getMovies()`, after our variable declarations.

  In the catch block, log any errors to the console. In the try block, use `fetch()` to send a GET request to `urlToFetch`. Await the response and save it to a variable called response.

- Log the `jsonResponse` object to the console. To see your output in the console, you will need to call `getMovies()` after the function declaration. In the console, you’ll see a key called `results` that holds an array of all the movies in the first page of results.

- Below our `jsonResponse` variable declaration in the if statement, store the `results` property of `jsonResponse` in a variable called `movies`. Log this variable to the console to confirm that it contains the correct information.

  Return `movies` as the last line of the if statement. Later on, we’ll use this list to select a random movie as a suggestion.

  After you check what movies logs to the console, remove the `getMovies()` function call. Otherwise, it will automatically execute every time you run your program, causing unexpected behavior later.

# Get Movie Info
## Instructions

- For the next several steps, we’ll be working inside the `getMovieInfo()` function to fetch the details of a random movie from the list of movies we returned in `getMovies()`.

- Modify `getMovieInfo()` by having it accept a parameter, `movie`. Then, inside the function, create a variable called `movieId` that is set to the `id` property of the movie parameter. We will be using the `id` property to make another call to the TMDB API

- Reference the [TMDB documentation](https://developers.themoviedb.org/3/discover/movie-discover) to find the movie “Details” endpoint. Save it to a variable called `movieEndpoint` and replace `{movie_id}` in the endpoint with our movieId variable.

- Let’s create our query params and the URL where we’ll send our `fetch()` request. Create a variable called `requestParams` and set it to be a query string with one parameter with `api_key` set to `tmdbKey`.

  Create a variable called `urlToFetch`. Set it equal to a string that consists of `tmdbBaseUrl`, followed by `movieEndpoint`, then `requestParams`.

- Turn `getMovieInfo()` into an asynchronous function that returns a promise. Add a try/catch block inside `getMovieInfo()`, after our variable declarations.

  In the catch block, log any errors to the console. In the try block, use `fetch()` to send a GET request to `urlToFetch`. Await the `response` and save it to a variable called `response`.

- Our response contains a single object with details about the given movie. Inside the if statement, convert this response to a JSON object. Await the resolution of this method, and save it to a variable called `movieInfo`

  Return `movieInfo` as the last line of the if block

  We can return our entire response object since it contains all the details for a single movie.

# Display Movie
## Instructions

- Turn `showRandomMovie()` into an asynchronous function. Then, on the last line of the function, call `getMovies()`, await its return, and save it to a variable called `movies`. Since `getMovies()` returns a promise, we need to `await` its resolution so that we can do something with its return value in upcoming steps.
- Below our `movies` declaration, call `getRandomMovie()`, passing `movies` as the argument. Store the returned value in a variable called `randomMovie`
- Below our `randomMovie` declaration, call `getMovieInfo()`, passing `randomMovie` as the argument. Await its return and save it to a variable called `info`.
- Finally, as the last line of the `showRandomMovie()` function, call `displayMovie()`, passing `info` as the argument.

  ### Run your program to see movie suggestions. Like or dislike each movie to be shown another random suggestion. Change genres to get different suggestions based on your interests!
