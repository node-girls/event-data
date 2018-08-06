# Events Data
JSON data containing all events for the London chapter.  Used to power the Node Girls website.

Full instructions on how to update the website [here](https://github.com/node-girls/node-girls-website/blob/master/updating-site.md)

## Data structure

An event object has the following structure:

```js
{
  "city": "",
  "date": "YYYY-MM-DD", // hyphens required
  "start_time": "HH:mm", // 24hr clock, with colon (:) and leading zero
  "end_time": "HH:mm",
  "title": "",
  "synopsis": "",
  "application_data": {
    "application_link": "",
    "application_text": "",
  },
  "venue": "",
  "sponsors": [ // always an array, in case of multiple sponsors
    {
      "name": "",
      "link": "valid url",
      "logo": "image url - remote or local file"
    }
  ]
}
```

Note: you might want line breaks for `application_text` or `synopsis`. Use `<br/>` as part of your string and it will be parsed correctly.

#### `city`
The chapter in question

#### `date`
Date of the event.  **Must** be in the YYYY-MM-DD format, including hyphens.  This is parsed by Moment.js to generate a more friendly format.  It's also used by `js/template.js` to sort the data properly.

#### `start_time`, `end_time`
When the event is due to start and end.  This must be 24 hour clock format, with a leading zero where needed.
Valid: "18:00", "08:00"
Invalid: "6.00" (missing leading zero), "06.00" (missing colon), "17.00" (missing colon)

#### `title`
This is the name of the event, e.g. "Introduction to JavaScript"

#### `synopsis`
Space to go into detail about the event, who it's aimed at, what people will learn etc.

#### `application_data`
**Array** of objects, with each object containing `application_text` and `application_link`.  Multiple objects can be used if there are multiple application forms for one event, (e.g. one for students and one for mentors)
##### `application_link`
URL that points to wherever people should sign up.  Revert to "" when applications have closed.

##### `application_text`
General info about applying.  This could say one of 3 things:
1. Applications are not live yet
2. Applications are live (see below)
3. Applications have closed

`application_text` will need to be updated throughout the lifecycle of the event, so that the text actually tells people what's going on :)

** When live**
`application_text` is made into a hyperlink, using the value at `application_link`.

#### `venue`
Name of the good people who are hosting us

#### `sponsors`
An **array** of sponsor objects.  Sponsor object contains
- name
  name of the sponsor (might be the same as `venue`)
- link
  Url pointing to the sponsor's website
- logo
  An image of the sponsor's logo.  Can be a local image on the repo or something grabbed from online.
