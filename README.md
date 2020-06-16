# mvsendgrid
Front end to Sendgrid

# Dependency

mvdbtools

# Config

SAMPLE_CONFIG.JSON

This is the config file template.  It must be renamed to CONFIG.JSON.

```
{
  "username":"user name for sendgrid (requried for v2 apis",
  "password":"password for sendgrid (requried for v2 apis)",
  "apikey":"Api Key for v3 apis (none built yet)
}
```

# overview

Function: MVSENDGRID.API(OBJ)

This is the front end to any sendgrid function. It takes a object as shown below.
Currently we only support mailsend_v2 as it allows normal -F posts to attach
files.  The v3 is a pure rest function and you must transform attachments to
base64.  The issue here is some pick platforms (d3 for example) do not like large
strings.  V2 functions are POSTS and require the user name/password for the account.

     * OBJ
      * { "api":"mailsend_v2",
      *    "params": {
      *       "to": [
      *         {
      *           "email":"email address",
      *           "name":"Nice name"
      *         }
      *       ],
      *       "cc": [
      *         {
      *           "email":"email address",
      *           "name":"Nice name"
      *         }
      *       ],
      *       "bcc": [
      *         {
      *           "email":"email address",
      *           "name":"Nice name"
      *         }
      *       ],
      *       "replyto":"address",
      *       "from":"From email address",
      *       "fromname":"From name",
      *       "subject":"Subject",
      *       "text":"Plain text of your email",
      *       "html":"Html version of your email",
      *       "files": [
      *           {
      *              "sourcefile":"path to file",
      *              "filename":"file name to present file as",
      *              "type":"type of file, application/pdf for example"
      *           }
      *       ]
      *    },
      *   "result": {
      *      "status":"error or ok", /* This is status msg from Sendgrid or a http code, yea bad but it is legacy
      *      "statusmsg:"status msg",
      *      "wcalldebug": "wcall object", /* html from original curl statement */
      *    }
      *
      *  }
      *
      * Starting with mailsend_v2 - We are using this version because it allows
      * attachments without having to base64 and include them into the json payload
      * v2 uses curl and a normal form-data post to get attachments.
      *
