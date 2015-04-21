
## Curl 7.41.0 (stable)

                                  _   _ ____  _
                              ___| | | |  _ \| |
                             / __| | | | |_) | |
                            | (__| |_| |  _ <| |___
                             \___|\___/|_| \_\_____|

With support for OpenSSL 1.0.2.
Tested on Windows (MinGW and Visual Studio), Linux gcc and OSX clang.

## How to use it?

New with biicode? Check the [getting started guide](http://docs.biicode.com/c++/gettingstarted.html).

Create new biicode project:
    
    > bii init myproject -l # Simplified layout

Create a *main.c* in myproject folder and paste contents:

    #include <stdio.h>
    #include <curl/curl.h>
    
    int main(void)
    {
      CURL *curl;
      CURLcode res;
    
      curl = curl_easy_init();
      if(curl) {
        curl_easy_setopt(curl, CURLOPT_URL, "http://example.com");
        /* example.com is redirected, so we tell libcurl to follow redirection */
        curl_easy_setopt(curl, CURLOPT_FOLLOWLOCATION, 1L);
    
        /* Perform the request, res will get the return code */
        res = curl_easy_perform(curl);
        /* Check for errors */
        if(res != CURLE_OK)
          fprintf(stderr, "curl_easy_perform() failed: %s\n",
                  curl_easy_strerror(res));
    
        /* always cleanup */
        curl_easy_cleanup(curl);
      }
      return 0;
    }

If you execute *bii build* command will fail because it doesn't find our curl dependency:

     fatal error: curl/curl.h: No such file or directory
     #include <curl/curl.h>

So lets wire it! Open **biicode.conf** file and put a requirement to this block and an include mapping to tell biicode where to find curl.h:

    [requirements]
    lasote/curl: 2 # We depend on lasote/curl block, check the last stable version, now is 2
    
    [includes]
    curl/*.h: lasote/curl/include

Build it! 

    > bii cpp:build

You can check a lot of [examples](http://www.biicode.com/examples/examples/curl/master) here: http://www.biicode.com/examples/examples/curl/master

