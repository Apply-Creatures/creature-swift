FROM woodpeckerci/woodpecker-server:next-b8b6efb352

EXPOSE 8000 9000 443

ENV WOODPECKER_GITHUB_URL=https://github.com
ENV WOODPECKER_GITHUB=true
ENV WOODPECKER_ADMIN=hirako2000
ENV WOODPECKER_REPO_OWNERS=Apply-Creatures

ENV WOODPECKER_WEBHOOK_HOST=https://ci.applycreatures.com
ENV WOODPECKER_HOST=https://ci.applycreatures.com

ENV WOODPECKER_OPEN=true

#ENV WOODPECKER_ORGS=apply-creatures # if enabled, it auto allow, but then cannot be let in the admin?
# it says can't find org of the @username

ENV WOODPECKER_CUSTOM_CSS_FILE=/usr/local/www/woodpecker.css
ENV WOODPECKER_CUSTOM_JS_FILE=/usr/local/www/woodpecker.js

COPY ./src /usr/local/www/

ENTRYPOINT ["/bin/woodpecker-server"]