# IRC

## Bouncers

* [ZNC](https://wiki.znc.in/ZNC) - feature-heavy mainstay
* [soju](https://sr.ht/~emersion/soju/) - sourcehut bouncer
* [chat.sr.ht](chat.sr.ht) - sourcehut cloud-hosted bouncer

## Command Line Clients

* `weechat`
  * servers
    * add server
      ```
      /server add libera irc.libera.chat -ssl
      ```
      Where `libera` is the `server name` to use
    * connect to server
      ```
      /connect [server name]
      ```
    * autojoin server
      ```
      /set irc.server.[server name].autoconnect on
      /save
      ```
  * channels
    * join channel
      ```
      /join #chat
      ```
    * autojoin channel
      ```
      /set irc.server.freenode.autojoin "#chat,#rant"
      /save
      ```
    * moving between channels
      ```
      /buffer [number next to channel name]
      ```
      * use ctl-p (prev) and ctl-n (next)
      * use alt-arrow keys
  * chat
    * to ping someone in chat, start typing their name and hit <tab>
    * to pm someone
      ```
      /query [user] message
      ```
