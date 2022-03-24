# censonemr
CENSON EMR
Add following to NGINX config file....
}
	if (!-e $request_filename) {
            # Needed for zend to work
            rewrite ^(.*/zend_modules/public)(.*) $1/index.php?$is_args$args last;
            # Needed for patient portal to work
            rewrite ^(.*/portal/patient)(.*) $1/index.php?_REWRITE_COMMAND=$1$2 last;
            # Needed for REST API/FHIR to work
            rewrite ^(.*/apis/)(.*) $1/dispatch.php?_REWRITE_COMMAND=$2 last;
            # Needed for OAuth2 to work
            rewrite ^(.*/oauth2/)(.*) $1/authorize.php?_REWRITE_COMMAND=$2 last;
        }
	fastcgi_split_path_info ^(.+\.php)(/.+)$;
	location /cgi-bin/ {
