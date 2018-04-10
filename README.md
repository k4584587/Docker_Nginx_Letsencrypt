# Docker + Nginx + Let's Encrypt

Let's Encrypt 인증서 발급

    $ docker run -it --rm \
	-v /home/letsencrypt:/etc/letsencrypt \
	-v /home/letsencrypt/var/lib/letsencrypt:/var/lib/letsencrypt \
	-v /home/admin/public_html:/data/letsencrypt \
	-v "/home/letsencrypt/ssl/var/log/letsencrypt:/var/log/letsencrypt" \
	certbot/certbot \
	certonly --webroot \
	--register-unsafely-without-email --agree-tos \
	--webroot-path=/data/letsencrypt \
	--staging \
	-d "foot.bar.com"


와일드 카드 SSL 발급

    $ docker run -it --rm --name letsencrypt \
    -v "/home/admin/letsencrypt:/etc/letsencrypt" \
    -v "/home/admin/letsencrypt/lib/letsencrypt:/var/lib/letsencrypt" \
    quay.io/letsencrypt/letsencrypt:latest \
        certonly \
        -d *.example.com \
        --manual \
        --preferred-challenges dns \
        --server https://acme-v02.api.letsencrypt.org/directory

Nginx Server Start

    $ docker-compose up -d --build
