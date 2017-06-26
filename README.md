
# Node-RED Workshop Hands-Out

 _Program the Bluemix Innovation Platform without writing code!_

_Try some Watson / Bluemix Services_

## Prerequisites:         

Bluemix Account, Browser (not Internet Explorer) 

Link to Bluemix console:   [console.ng.bluemix.net](https://console.ng.bluemix.net)

**We will use Bluemix US for this workshop!**

Make sure that:

![bmx org](doc_img/bmx_org.jpg)

## Login to Bluemix & Create Node-RED  runetime

Go to catalog and create the "Node-RED starter" application ( Boilerplates Section )

![bmx starter](doc_img/bmx_nodeRED_starter.jpg)
 
you must give it a **unique name** ( this name is your hostname and so needs to be unique across Bluemix.)

( I use:  [**red-mh** - _mybluemix.net_](https://red-mh.mybluemix.net) )


## Basic Flow with twitter &  Bluemix / Cloudant database

URL for non twitter users:  ```ws://red-mh.mybluemix.net/twitter```

![twitter_flow](doc_img/twitter_flow.jpg)

/getdb  template code (mustache):

```json
{{#payload}}<li>{{payload}}</li>{{/payload}}    ```
( Option if time: install dashboard via "manage palette"  -  add  and configure dashboard nodes  )


##Watson Tone-Analyzer

![tone_ana](doc_img/tone_ana.jpg)


template code (mustache)  :scissors: :

```json
{{#response.document_tone.tone_categories}}
{{category_name}}
------------------
{{#tones}}
{{tone_name}}       {{score}}
{{/tones}}

{{/response.document_tone.tone_categories}}
```


##Watson Visual Recogintion##

Insert Flow code:

```json
tt
```

Sample image url:


https://red-mh.mybluemix.net/img?img=lhjumbo.jpg



https://red-mh.mybluemix.net/img?img=lha330.jpg