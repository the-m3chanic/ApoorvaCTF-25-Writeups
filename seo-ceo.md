# SEO CEO 

<loc>https://www.thiswebsite.com/goofyahhroute</loc>

This suggested that there was a hidden route called "goofyahhroute" on the target website.

## Exploitation Approach

### Step-by-Step Exploitation

1. Access the sitemap.xml file at https://seo-opal.vercel.app/sitemap.xml
2. Identify the hidden route mentioned in the sitemap: `/goofyahhroute`
3. Navigate to https://seo-opal.vercel.app/goofyahhroute
4. Receive a message: "ok bro u da seo master gng frfr ngl no cap but do you really want the "flag"? come on blud, it's a yes or no question yeah?"
5. Determine that the message is asking for a parameter related to "flag" with a yes/no value
6. Append the parameter `?flag=yes` to the URL: https://seo-opal.vercel.app/goofyahhroute?flag=yes

## Flag

Upon successfully accessing the correct endpoint with the correct parameter, we received the flag:
```
apoorvctf{s30_1snT_0pt1onaL}
```

## Tools Used
- Web browser
- Basic knowledge of XML sitemaps and URL parameters

## Conclusion

This challenge highlighted the importance of examining SEO-related files like sitemap.xml for potential information disclosure. The challenge demonstrated how sitemaps can inadvertently reveal hidden routes and functionality, and how simple parameter testing can lead to discovering flags.

The name "SEO CEO" itself was a hint pointing toward the sitemap.xml file, which is a common SEO tool used by websites to help search engines discover and index content.