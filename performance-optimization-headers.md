# Cache Control and Performance Headers
# Add these to your web server configuration or hosting provider

## For Apache (.htaccess)
<IfModule mod_expires.c>
    ExpiresActive On
    
    # Images - 1 year
    ExpiresByType image/jpg "access plus 1 year"
    ExpiresByType image/jpeg "access plus 1 year"
    ExpiresByType image/gif "access plus 1 year"
    ExpiresByType image/png "access plus 1 year"
    ExpiresByType image/webp "access plus 1 year"
    ExpiresByType image/avif "access plus 1 year"
    ExpiresByType image/svg+xml "access plus 1 year"
    
    # CSS and JS - 1 year
    ExpiresByType text/css "access plus 1 year"
    ExpiresByType application/javascript "access plus 1 year"
    
    # Fonts - 1 year
    ExpiresByType font/woff "access plus 1 year"
    ExpiresByType font/woff2 "access plus 1 year"
    ExpiresByType application/font-woff "access plus 1 year"
    
    # HTML - 1 day
    ExpiresByType text/html "access plus 1 day"
</IfModule>

<IfModule mod_headers.c>
    # Cache control for static assets
    <FilesMatch "\\.(ico|pdf|flv|jpg|jpeg|png|gif|webp|avif|js|css|swf|woff|woff2)$">
        Header set Cache-Control "max-age=31536000, public, immutable"
    </FilesMatch>
    
    # Cache control for HTML
    <FilesMatch "\\.(html|htm)$">
        Header set Cache-Control "max-age=86400, public"
    </FilesMatch>
    
    # Preconnect hints
    Header add Link "</assets/css/main.css>; rel=preload; as=style"
    Header add Link "<https://cdn.jsdelivr.net>; rel=preconnect; crossorigin"
</IfModule>

## For Nginx
# Add to your nginx.conf or site configuration

location ~* \.(jpg|jpeg|png|gif|webp|avif|ico|svg)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}

location ~* \.(css|js|woff|woff2)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}

location ~* \.(html|htm)$ {
    expires 1d;
    add_header Cache-Control "public";
}

## For GitHub Pages
# Add _headers file to root directory with content:
# /*
#   Cache-Control: max-age=31536000
# /*.html
#   Cache-Control: max-age=86400