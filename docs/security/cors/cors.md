# CORS

## What is CORS?

Cross-origin resource sharing (CORS) is a mechanism for integrating applications.  
CORS defines a way for client web applications that are loaded in one domain to interact with resources in a different domain.

This is useful because complex applications often reference third-party APIs and resources in their client-side code.  
For example, your application may use your browser to pull videos from a video platform API, use fonts from a public font library, or display weather data from a national weather database.

<!-- CORS allows the client browser to check with the third-party servers if the request is authorized before any data transfers. -->

## Why is Cross-Origin Resource Sharing Important?

In the past, when internet technologies were still new,  
cross-site request forgery (CSRF) issues happened.  
These issues sent fake client requests from the victim's browser to another application.

For example, the victim logged into their bank's application.  
Then they were tricked into loading an external website on a new browser tab.  
The external website then used the victim's cookie credentials and relayed data to the bank application while pretending to be the victim.  
Unauthorized users then had unintended access to the bank application.

To prevent such CSRF issues, all browsers now implement the same-origin policy.

## Same-origin Policy

Today, browsers enforce that clients can only send requests to a resource with the same origin as the client's URL.  
The protocol, port, and hostname of the client's URL should all match the server it requests.

For example, consider the origin comparison for the below URLs with the client URL `http://store.aws.com/dir/page.html`.

| URL                                         | Outcome          | Reason                                         |
| ------------------------------------------- | ---------------- | ---------------------------------------------- |
| `http://store.aws.com/dir2/new.html`        | Same origin      | Only the path differs                          |
| `http://store.aws.com/dir/inner/other.html` | Same origin      | Only the path differs                          |
| `https://store.aws.com/page.html`           | Different origin | Different protocol                             |
| `http://store.aws.com:81/dir/page.html`     | Different origin | Different port (http:// is port 80 by default) |
| `http://news.aws.com/dir/page.html`         | Different origin | Different host                                 |

So, the same-origin policy is highly secure but inflexible for genuine use cases.

Cross-origin resource sharing (CORS) is an extension of the same-origin policy.  
You need it for authorized resource sharing with external third parties.  
For example, you need CORS when you want to pull data from external APIs that are public or authorized.  
You also need CORS if you want to allow authorized third-party access to your own server resources.

## How Does Cross-Origin Resource Sharing Work?

In standard internet communication,  
Your browser sends an HTTP request to the application server, receives data as an HTTP response, and displays it.

In browser terminology, the current browser URL is called the current origin and the third-party URL is cross-origin.

When you make a cross-origin request, this is the request-response process:

1. The browser adds an origin header to the request with information about the current origin's protocol, host, and port
1. The server checks the current origin header and responds with the requested data and an Access-Control-Allow-Origin header
1. The browser sees the access control request headers and shares the returned data with the client application

Alternatively, if the server doesn’t want to allow cross-origin access, it responds with an error message.

### Cross-Origin Resource Sharing Example

For example, consider a site called `https://news.example.com`.  
This site wants to access resources from an API at `https://partner-api.com`.

Developers at `https://partner-api.com` first configure the cross-origin resource sharing (CORS) headers on their server,  
by adding `https://news.example.com` to the allowed origins list.

Once CORS access is configured, `https://news.example.com` can request resources from `https://partner-api.com`.  
For every request, `https://partner-api.com` will respond with `Access-Control-Allow-Credentials : "true"`  
The browser then knows the communication is authorized and permits cross-origin access.

## References

- [aws.amazon.com](https://aws.amazon.com/what-is/cross-origin-resource-sharing/)

## Read More

- https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
- https://en.wikipedia.org/wiki/Cross-origin_resource_sharing
- https://portswigger.net/web-security/cors
- https://auth0.com/blog/cors-tutorial-a-guide-to-cross-origin-resource-sharing/
- https://web.dev/articles/cross-origin-resource-sharing
