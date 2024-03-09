# Используйте образ с поддержкой Rust
FROM rust:alpine as builder

# Установка рабочей директории
WORKDIR /usr/src/my_prog

# Копирование зависимостей и файлов проекта
COPY Cargo.toml Cargo.lock ./
COPY src ./src

# Сборка приложения
RUN cargo build --release
# Проверка тестов
RUN cargo test || exit 1

# Окончательная сборка контейнера
FROM alpine:latest

# Установка окружения и копирование бинарного файла из предыдущего этапа
COPY --from=builder /usr/src/my_prog/target/release/check_docker /usr/local/bin/check_docker

# Запуск приложения при старте контейнера
CMD ["check_docker"]