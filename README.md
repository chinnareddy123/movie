# movie
Html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Movie App</title>
    <link rel="stylesheet" href="style.css">
    <script src="app.js" defer></script>
</head>
<body>
  <!-- The header that contains the title and the Search bar -->
    <header>
        <a href="#"><h1>Movies</h1></a>
        <form id="form">
            <input
                type="text"
                id="search"
                placeholder="Search"
                class="search"
            />
        </form>
    </header>
  <!-- The main tag where we are going to put all our movies that we got from the API -->
    <main id="main"></main>
</body>
</html>
#Css
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
body{
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
}
header{
    width: 100%;
    height: 50px;
    background: rgb(38, 39, 38);
    display: flex;
    align-items: center;
    justify-content: flex-start;
    border-bottom: 1px solid #ccc;
}
header h1{
    margin: 0 20px;
    color: #fff;
}
header a {
    text-decoration: none;
}
header form{
    display: flex;
    align-items: center;
}
/* The search bar */
#search{
    width: 230px;
    height: 30px;
    border: 1px solid black;
    outline: none;
    border-radius: 20px;
    padding-left: 15px;
}
#Javascript 
const apiUrl = 'https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=04c35731a5ee918f014970082a0088b1&page=1';
const IMGPATH = "https://image.tmdb.org/t/p/w1280";
const SEARCHAPI =
    "https://api.themoviedb.org/3/search/movie?&api_key=04c35731a5ee918f014970082a0088b1&query=";
// Selecting our Elements.
const main = document.getElementById("main");
const form = document.getElementById("form");
const search = document.getElementById("search");
/* call the showMovies function that requests the movie data from the Api using fetch.
 Then it puts those data in the main HTML tag by creating elments for those data. */
showMovies(apiUrl);
function showMovies(url){
    fetch(url).then(res => res.json())
    .then(function(data){
    data.results.forEach(element => {
      // Creating elemnts for our data inside the main tag. 
        const el = document.createElement('div');
        const image = document.createElement('img');
        const text = document.createElement('h2');
text.innerHTML = `${element.title}`;
        image.src = IMGPATH + element.poster_path;
        el.appendChild(image);
        el.appendChild(text);
        main.appendChild(el);
    }); 
});
}
form.addEventListener("submit", (e) => {
    e.preventDefault();
    main.innerHTML = '';
     
    const searchTerm = search.value;
 /* Adding the value wriiten in the search bar to the search Api,
    in order to get the movies we search for. */
    if (searchTerm) {
        showMovies(SEARCHAPI + searchTerm);
        search.value = "";
    }
});
#Styling movie
main{
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}
main div{
    width: 250px;
    height: 320px;
    margin: 19px 15px;
    background: red;
}
img{
    width: 100%;
    height: 89%;
    object-fit: cover;
}
h2{
    font-size: 20px;
    font-family: sans-serif;
    font-weight: bold;
    text-align: center;
    color: #fff;
}
