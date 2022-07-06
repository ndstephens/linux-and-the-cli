# `curl`

- Unlike `wget`, `curl` works more like a normal Linux program in that it operates on input and output streams. Because of this you can plug it into other programs.
  - **_`curl` is stream based_**
- `curl` can be used to do testing against API servers (similar to Postman).

## Output

- Redirect (replace or append) the contents of a file with the `curl` response:

```sh
curl <url> > <file-name>
```

- Or use a flag to redirect the output to a file:

```sh
curl -o <file-name> <url>
```

- If the `url` points to a file and you're okay saving that response as a file of the same name:

```sh
curl -O http://mydomain.com/my-file.txt
```

> Will be saved locally as `my-file.txt`

## HTTP Verbs

- To simply verify an endpoint is working you can send a `HEAD` request instead of a `GET` request:

```sh
curl -I <url> # or --head instead of -I
```

### POST

```sh
curl -X POST <url>
curl -d "this is the body being sent with the HTTP request" <url>
```

> The first one, `-X`, allows you to specify what verb you want to use. In this case we used POST.
>
> In the second case, because we're using `-d` to send a POST body, it implicitly sets the verb to POST as well.

```sh
curl -X PUT <url>
curl -X PATCH <url>
curl -X DELETE <url>
curl -X OPTIONS <url>
```

## Cookies

```sh
curl -b "foo=bar" <url>
```

> Cookie jar files can be useful too. It's just a file with all your cookies in it.
>
> If you're making a lot of requests and need to send a lot of cookies, you can put all of those into a file and use `-c <file-name>` to use those as your cookies.

## Redirect

```sh
curl http://bit.ly/linux-cli
```

> By default curl won't follow redirects.
>
> If you do `curl -L http://bit.ly/linux-cli` you'll tell curl to follow the redirect and you'll end up with the full site.

## Headers

- You'll use -H and you'll do one header per -H (meaning you'll need multiple -H to do multiple different headers).

```sh
curl -H "'accept-language: en-US" -H "Authorization: Bearer 12345" <url>
```

## Edge / Chrome / Firefox curls

- Modern browsers have the ability to copy requests out of your `network` panel in your dev tools as curl requests and then be able to replay them from the command line.
- You can do this to properly formulate requests and get all the auth headers right.

## `curl | bash`

- A lot of tutorials or installation of tools will have you do a request of `curl <url> | bash`.
- This will nab the contents of the URL off the network and pipe that directly into bash which will execute what's in the contents of the network request.
- **_THIS CAN BE VERY DANGEROUS._**
  - You're basically giving whoever controls that URL unlimited access to your computer.
- There's a few things to keep in mind when you do it:
  - Always read the script you're about to invoke. Be especially suspicious of them making more network requests or decoding `base64` strings.
  - Only do it from domains you trust. It's actually possible to detect a `curl` request as opposed to a browser request, meaning you can load the file in a browser and see something and then when you go to `curl` it they can serve you a different file. Basically means you should only do `curl | bash` from GitHub.
  - When in doubt just `curl <url> > file.sh` and then read the file. From there, `chmod 700 file.sh` and `. file.sh`. It's not that many more steps.

```sh
curl <url> > file.sh
chmod 700 file.sh
. file.sh
```
