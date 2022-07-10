# comment-key

```sh
npm install comment-key
```

comment-key will search through all your directories and files looking for comments with a specific syntax. Specifiy one directory and all inner directories and files will be checked. Increases developer productivity. Works well when using docker or github and sharing projects. Great for asking and answering questions and leaving contact info.

<br><br>
Comments must be written in this syntax..

```js
//^*^(your comment here)
```

```js
const comment_keys = require("comment-key");

const folders = [
  { folder: "./cron", files: "all" }, // { folder: './my_folder', files: ([]), ('all'), (['a.js', 'b.js']) }
  { folder: "./db", files: "all" }, // 'all' searches through all directories and files
  { folder: "./routes", files: "all" },
  { folder: "./public", files: "all" },
  { folder: "./views", files: "all" },
  { folder: "./", files: ["app.js"] },
];

var comments = [];

try {
  comments = comment_keys(folders);
} catch (err) {
  console.log(err.message);
}

for (let i = 0; i < comments.length; i++) {
  console.log(comments[i]);
  //linenumber
  //filepath
  //comment
}
```

# Use case

You are a manager going through all of your files and making updates. You write comments everywhere with the syntax (above) so that when your devs login, they see the list of comments and know where to go and what they need to do.
<br><br>
You are an express developer who writes comments as to do lists.
<br><br>
You are browsing through your code making sure everything is correct before release. You find a few bugs and write some comment keys.
<br><br>
Below each comment you should have a larger comment without the syntax that describes what the problem is in detail.

# How it works

Uses the file system module to traverse a set of directories looking for '//^\*^('. Once '//^\*^(' is found, the comment gets built up and is pushed to the comment set.
