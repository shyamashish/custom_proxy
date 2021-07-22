# custom_proxy and reverse proxy for mac users..

## generate a certificate and key
generate `private.crt` and `private.key` files using following command:

    openssl req -config ./ssl.conf -new -sha256 -newkey rsa:2048 -nodes -keyout private.key -x509 -days 3650 -out private.crt

##Import generated certificate into the Keychain and trust it:

    sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain private.crt

## build docker 
    docker build . -t custom-proxy-mytestvm

## run docker image
    docker run -p 80:80 -p 443:443 custom-proxy-mytestvm
