# Assignments

var XMLHttpRequest = require("xmlhttprequest").XMLHttpRequest
const inventors = [
  { first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },
  { first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 },
  { first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 },
  { first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },
  { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 },
  { first: 'Nicolaus', last: 'Copernicus', year: 1473, passed: 1543 },
  { first: 'Max', last: 'Planck', year: 1858, passed: 1947 },
  { first: 'Katherine', last: 'Blodgett', year: 1898, passed: 1979 },
  { first: 'Ada', last: 'Lovelace', year: 1815, passed: 1852 },
  { first: 'Sarah E.', last: 'Goode', year: 1855, passed: 1905 },
  { first: 'Lise', last: 'Meitner', year: 1878, passed: 1968 },
  { first: 'Hanna', last: 'Hammarström', year: 1829, passed: 1909 }
];



// 1. Filter the list of inventors for those who were born in the 1500's
// We are passing a function to filter which comparent birth year. We only
// allow the people who were born in 1500 >= year < 1600.
const filteredArray =  inventors.filter(inventor => inventor.year >= 1500 && inventor.year < 1600)
console.log(filteredArray) 

// 2. Give us an array of the inventors first and last names
// We use map to create array of first and last names of inventors. We pass
// a function to map which creates new array based on old array.
const namesOfInventors  
= inventors.map(inventor => `${inventor.first} ${inventor.last}`)
console.log(namesOfInventors)

// 3. Sort the inventors by birthdate, oldest to youngest
// We pass a function to sort that rearranges invetors based on their ages.
// We switch positions of inventors if firstInventor.year > secondInventor.year.
const sortedInventors = inventors.sort((inventorA, inventorB) => inventorA.year > inventorB.year ? inventorB : inventorA)

// 4. How many years did all the inventors live all together?
const totalYears = inventors.reduce((total, inventor) => (
  total + (inventor.passed - inventor.year)
), 0);
console.log (totalYears)

// 5. Sort the inventors by years lived
 const oldest = inventors.sort(function(a, b) {
      const lastInventor = a.passed - a.year;
      const nextInventor = b.passed - b.year;
      return lastInventor > nextInventor ? -1 : 1;
    });
    console.table(oldest);



// 6. create a list of Boulevards in Paris that contain 'de' anywhere in the name
// https://en.wikipedia.org/wiki/Category:Boulevards_in_Paris
//// https://en.wikipedia.org/wiki/Category:Boulevards_in_Paris
// Okay got it. We have to download the webpage from wikipedia and do a simple querySelectorAll
console.time('6. Boulevards');
const xhr = new XMLHttpRequest();

//ResponseType cannot be set on sync ajax requests
//xhr.responseType = "json";

xhr.open('get', 'https://en.wikipedia.org/w/api.php?action=query&format=json&origin=*&list=categorymembers&cmtitle=Category%3ABoulevards_in_Paris&cmlimit=max', false);

xhr.onreadystatechange = function() {
  const DONE = 4; // readyState 4 means the request is done.
  const OK = 200; // status 200 is a successful return.
  if (xhr.readyState === DONE) {
    if (xhr.status === OK) {
      const data = JSON.parse(xhr.response).query.categorymembers;
      const boulevards = data.map(cm => cm.title);

      const de = boulevards.filter(name => name.includes('de'));
      console.timeEnd('6. Boulevards');
      console.log(de);
    } else {
      console.log('Error: ' + xhr.status); // An error occurred during the request.
    }
  }
};
xhr.send();

// 7. sort Exercise
// Sort the people alphabetically by last name
const sortedArray = inventors.sort((inventor1, inventor2) => 
	inventor1.last > inventor2.last ? -1 : 1
)
console.log(sortedArray)
// Have you completed the others?
// 8. Reduce Exercise
// Sum up the instances of each of these

const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck' ];

const transportation = data.reduce(function(obj, item) {
      if (!obj[item]) {
        obj[item] = 0;
      }
      obj[item]++;
      return obj;
    }, {});

    console.log(transportation);


// data for next few questions
const people1 = [
  { name: 'Wes', year: 1988 },
  { name: 'Kait', year: 1986 },
  { name: 'Irv', year: 1970 },
  { name: 'Lux', year: 2015 }
];

const comments = [
  { text: 'Love this!', id: 523423 },
  { text: 'Super good', id: 823423 },
  { text: 'You are the best', id: 2039842 },
  { text: 'Ramen is my fav food ever', id: 123523 },
  { text: 'Nice Nice Nice!', id: 542328 }
];

// 9. Some and Every Checks
// Array.prototype.some() // is at least one person 19?
const is19 = people1.some(person => (2021 - parseInt(person.year)) >= 19)
console.log(is19) //true//

// 10. Array.prototype.every() // is everyone 19?
const isEveryone19 = people1.every(person => (2021 - parseInt(person.year)) >= 19)
console.log(`Everyone is ${isEveryone19 ? '' : 'not'} at least 19.`)

//checks variable condion extract 
// 11. Array.prototype.find() array search
// Find is like filter, but instead returns just the one
// find the comment with the ID of 823423
const comment = comments.find(comment => comment.id === 823423);
 console.log(comment);

// 12. Array.prototype.findIndex() built in function 
// Find the comment with this ID
// deleted the comment with the ID of 823423
const index = comments.findIndex(comment => comment.id === 823423);
    console.log(index);
   // comments.splice(index, 1);
    const newComments = [
      ...comments.slice(0, index),
      ...comments.slice(index + 1)
    ]
