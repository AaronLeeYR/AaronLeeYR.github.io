# AaronLeeYR.github.io

<h1>1.Go to the folder where you want to store your project, and clone the new repository:
git clone https://github.com/username/username.github.io

<h1>2.Enter the project folder and add an index.html file:
cd username.github.io
echo "Hello World" > index.html

<h1>3.Add, commit, and push your changes:
git add --all
git commit -m "Initial commit"
git push -u origin main

Git Repo:   https://github.com/AaronLeeYR/AaronLeeYR.github.io
Live Site:  https://aaronleeyr.github.io/


CSS

* {
  box-sizing: border-box;
}

.left {
  background-color: skyblue;
  padding: 20px;
  float: left;
  width: 30%; /* The width is 20%, by default */
  Height: 300px
}

.main {
  background-color: yellow;
  padding: 20px;
  float: left;
  width: 40%; /* The width is 60%, by default */
  Height: 300px
}

.right {
  background-color: green;
  padding: 20px;
  float: left;
  width: 30%; /* The width is 20%, by default */
  Height: 300px
}

/* Use a media query to add a break point at 800px: */
@media screen and (max-width: 800px) {
  .left, .main, .right {
    width: 100%; /* The width is 100%, when the viewport is 800px or smaller */
  }
}

#container {
  background: white;
  width: 800px;
  margin: 0 auto; /* how you centre align a box 
                     / non-text */
  margin-top: 50px;
  border: 10px solid pink;
}

h1{
  text-align: center;
}
