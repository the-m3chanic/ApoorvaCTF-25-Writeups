# Blog-1 

## Challenge Overview
The challenge involves exploiting a race condition vulnerability in a web application to bypass a restriction that requires creating 5 blogs before accessing the `/api/v2/gift` endpoint, which contains the flag.

## Discovery & Reconnaissance

Initial reconnaissance revealed several API endpoints:
- `/api/v2/gift` - Requires 5 blogs to access, contains the flag
- `/api/v1/blog/comment/<slug>` - Endpoint for commenting on blogs
- `/api/v1/blog/getAll` - Endpoint to retrieve all blogs
- `/api/v1/blog/login` - Login endpoint
- `/api/v1/blog/register` - Registration endpoint
- `/api/v1/blog/addBlog` - Endpoint to create a blog (discovered during testing)

The challenge hint was that we need 5 blogs before accessing the gift endpoint.

## Vulnerability Identification

The key observation was the API versioning: `/api/v2/gift` suggests there might be a `/api/v1/gift` endpoint as well.

However, the core vulnerability is a **race condition** in the blog creation process. The application doesn't properly handle concurrent requests, allowing us to create multiple blogs simultaneously by exploiting this race condition.

## Exploitation Approach

### Race Condition Exploitation

To exploit the race condition, we need to:
1. Register an account
2. Send multiple blog creation requests simultaneously 
3. Use Burp Suite's "Send Group in Parallel (use last-byte synchronization)" feature

### Step-by-Step Exploitation

1. Register a new user account using the `/api/v1/blog/register` endpoint
2. Log in with the created account via `/api/v1/blog/login`
3. Configure Burp Suite to intercept requests
4. Create a single legitimate blog post request to the `/api/v1/blog/addBlog` endpoint
5. In Burp Suite:
   - Send the request to Repeater
   - Duplicate the request tab multiple times (at least 5)
   - Select all tabs
   - Right-click and choose "Send Group in Parallel (use last-byte synchronization)"
   
6. The race condition allows multiple blog posts to be created simultaneously
7. Once we have 5+ blogs created, access the `/api/v2/gift` endpoint to retrieve the flag

### Key Insight

During testing, we discovered that changing the endpoint from `/api/v2/gift` to `/api/v1/gift` also revealed the flag, suggesting that the version check was only implemented in the front-end or was bypassed.

## Flag

Upon successfully exploiting the race condition and accessing the gift endpoint, we received:

```
Congratulations! You received a special gift: https://youtu.be/WePNs-G7puA?si=DOUFW9vAgUKdClxX
apoorvctf{s1gm@_s1gm@_b0y}
```

## Tools Used
- Burp Suite (for intercepting and modifying requests)
- Parallel request feature with last-byte synchronization (crucial for exploiting the race condition)

## Conclusion

This challenge taught us the importance of proper synchronization in web applications. The race condition allowed us to bypass a restriction meant to limit access to the flag endpoint by creating multiple blog posts simultaneously.