---
title: "Making a Calendar With Javascript and Tailwindcss"
date: 2023-02-14T12:29:39+02:00
draft: false
toc: false
images:
tags:
  "javaScript"
---

## Assumptions

This Guide assume you are not a beginner and are familiar with javascript with tailwindcss

## How To

### Create a table with two rows

- The first row is the header row for marking days from Sunday to Saturday
- The second row is what we will use to place the first day of month

The html should look like something like this :

``` html
  <table class="text-center">
    <thead>
        <tr>
            <th class="px-4 py-2">Sun</th>
            <th class="px-4 py-2">Mon</th>
            <th class="px-4 py-2">Tue</th>
            <th class="px-4 py-2">Wed</th>
            <th class="px-4 py-2">Thu</th>
            <th class="px-4 py-2">Fri</th>
            <th class="px-4 py-2">Sat</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td class="px-4 py-2"></td>
            <td class="px-4 py-2"></td>
            <td class="px-4 py-2"></td>
            <td class="px-4 py-2"></td>
            <td class="px-4 py-2"></td>
            <td class="px-4 py-2"></td>
            <td class="px-4 py-2"></td>
        </tr>

    </tbody>
  </table>
```

### Creating the rest of the rows

in our javascript code, First we have to query today's month, year and days in a month.

```javascript
  const now = new Date();
  const currentMonth = now.getMonth();
  const currentYear = now.getFullYear();
  const daysInMonth = new Date(currentYear, currentMonth + 1, 0).getDate();
```

We will use a for-loop to iterate over the days in the month and also filling the calendar.

Initially we have to fill the first row, which is what determines on what day does the month start. This can be achieved by the following block of code:

```javascript


  let new_row = false; //checks if we are past the first row

 for (let i = 0; i < daysInMonth; i++) {

  // calculate the day of the week
  let day = new Date(currentYear, currentMonth, i + 1).getDay();

    // executes when we are still in the first week
   if(!new_row){

    // query the first row cell
    let cell = document.querySelector(`td:nth-child(${day + 1 })`);
                      
      
      // populate the cell with the date
      cell.textContent = i + 1;

      // when its past the first week toggle new_row to true
      if(day === 6){
          new_row = !new_row;
      }
    }

 }

```

When the first row/week is filled, add another row and fill in corresponding dates

```javascript
  day = day + 6
  document.querySelector('tbody').insertAdjacentHTML('beforeend',(`
      <tr>
          <td class="px-4 py-2">${i+1 <= daysInMonth ? i+1 : ''}</td>
          <td class="px-4 py-2">${i+2 <= daysInMonth ? i+2 : ''}</td>
          <td class="px-4 py-2">${i+3 <= daysInMonth ? i+3 : ''}</td>
          <td class="px-4 py-2">${i+4 <= daysInMonth ? i+4 : ''}</td>
          <td class="px-4 py-2">${i+5 <= daysInMonth ? i+5 : ''}</td>
          <td class="px-4 py-2">${i+6 <= daysInMonth ? i+6 : ''}</td>
          <td class="px-4 py-2">${i+7 <= daysInMonth ? i+7 : ''}</td>
      </tr>
  `))
  i += 6;
```

To make sure dates past the days in the month are not being filled, a conditional statement is required :

```javascript
  {i+dayOfTheWeek <= daysInMonth ? i+dayOfTheWeek : ''}
```

This is the how the Whole javascript code should look like

```javascript
  const now = new Date();
  const currentMonth = now.getMonth();
  const currentYear = now.getFullYear();
  const daysInMonth = new Date(currentYear, currentMonth + 1, 0).getDate();

  let new_row = false; //checks if we are past the first row

 for (let i = 0; i < daysInMonth; i++) {

  // calculate the day of the week
  let day = new Date(currentYear, currentMonth, i + 1).getDay();

    // executes when we are still in the first week
   if(!new_row){

    // query the first row cell
    let cell = document.querySelector(`td:nth-child(${day + 1 })`);
                      
      
      // populate the cell with the date
      cell.textContent = i + 1;

      // when its past the first week toggle new_row to true
      if(day === 6){
          new_row = !new_row;
      }
    }else{
        day = day + 6
        document.querySelector('tbody').insertAdjacentHTML('beforeend',(`
            <tr>
                <td class="px-4 py-2">${i+1 <= daysInMonth ? i+1 : ''}</td>
                <td class="px-4 py-2">${i+2 <= daysInMonth ? i+2 : ''}</td>
                <td class="px-4 py-2">${i+3 <= daysInMonth ? i+3 : ''}</td>
                <td class="px-4 py-2">${i+4 <= daysInMonth ? i+4 : ''}</td>
                <td class="px-4 py-2">${i+5 <= daysInMonth ? i+5 : ''}</td>
                <td class="px-4 py-2">${i+6 <= daysInMonth ? i+6 : ''}</td>
                <td class="px-4 py-2">${i+7 <= daysInMonth ? i+7 : ''}</td>
            </tr>
        `))
        i += 6;
    }

 }
```

Check out the repository on [Github](https://github.com/PrinceMwase/tailwindcss_javascript_calendar) and feel free to contribute