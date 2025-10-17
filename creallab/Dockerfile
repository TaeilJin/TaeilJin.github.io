FROM ruby:latest

LABEL maintainer="Taeil Jin <your.email@example.com>"
ENV DEBIAN_FRONTEND=noninteractive

# --- 필수 패키지 설치 ---
RUN apt-get update -y && apt-get install -y --no-install-recommends \
    locales \
    nodejs npm \
    imagemagick \
    build-essential \
    zlib1g-dev \
    python3-pip \
    inotify-tools procps && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/* && \
    pip install nbconvert --break-system-packages

# --- 로케일 설정 ---
RUN sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen && locale-gen

ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8 \
    JEKYLL_ENV=production

# --- 작업 디렉토리 설정 ---
WORKDIR /srv/jekyll

# --- Gemfile 복사 및 의존성 설치 ---
COPY Gemfile Gemfile.lock ./
RUN gem install jekyll bundler && bundle install --no-cache

# --- 포트 개방 ---
EXPOSE 8080

# --- Jekyll 서버 실행 ---
CMD ["bundle", "exec", "jekyll", "serve", "--host", "0.0.0.0", "--port", "8080"]
