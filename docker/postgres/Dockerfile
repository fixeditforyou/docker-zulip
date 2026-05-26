# See https://github.com/zulip/zulip/blob/main/Dockerfile-postgresql

ARG PGROONGA_VERSION=latest
ARG POSTGRESQL_VERSION=18
FROM groonga/pgroonga:$PGROONGA_VERSION-alpine-$POSTGRESQL_VERSION-slim

RUN apk add -U --no-cache hunspell-en
RUN ln -sf /usr/share/hunspell/en_US.dic /usr/local/share/postgresql/tsearch_data/en_us.dict && ln -sf /usr/share/hunspell/en_US.aff /usr/local/share/postgresql/tsearch_data/en_us.affix

COPY --from=zulip/zulip-postgresql:14 /usr/local/share/postgresql/tsearch_data/zulip_english.stop /usr/local/share/postgresql/tsearch_data/
COPY --from=zulip/zulip-postgresql:14 /docker-entrypoint-initdb.d/zulip-create-db.sql /docker-entrypoint-initdb.d/
COPY --from=zulip/zulip-postgresql:14 /docker-entrypoint-initdb.d/zulip-create-pgroonga.sql /docker-entrypoint-initdb.d/
