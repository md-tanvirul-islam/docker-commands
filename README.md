# 🐳 My Docker Journey

## 🚀 Docker Workflow

```
Dockerfile → build → Docker Image → run → Docker Container
```

---

## 📄 What is a Dockerfile?

A **Dockerfile** contains instructions for building a Docker image.

---

## 📦 What is Build Context in Docker?

When using the `docker build` command, Docker sends the entire directory (where the Dockerfile resides) as the **build context** to the Docker engine. This includes the Dockerfile and all sibling files/folders.

> 🔒 Docker **cannot access files outside** the build context.

---

## 🧾 Dockerfile Instructions

### `FROM`
- Specifies the **base image**.
- Always prefer **versioned tags** over `latest`.

```Dockerfile
FROM node:18-alpine
```

---

### `WORKDIR`
- Sets the **working directory** in the image filesystem.
- All subsequent commands execute in this directory.

```Dockerfile
WORKDIR /app
```

---

### `COPY`
- Copies files from **host** to **image**.
- Cannot copy files outside of the current directory.

```Dockerfile
COPY package.json /app
COPY package.json README.md /app/
COPY package*.json /app/
COPY . /app/
COPY ["hello world.txt", "."]
```

---

### `ADD`
- Works like `COPY` but:
  - Can **download from URLs**.
  - Can **auto-extract** compressed files.

```Dockerfile
ADD https://xyz.com/abc.json .
ADD file.zip .
```

---

### `RUN`
- Executes **commands at build time**.

```Dockerfile
RUN npm install
```

---

### `ENV`
- Sets environment variables.

```Dockerfile
ENV APP_VERSION=10
# View with:
# printenv APP_VERSION
# echo $APP_VERSION
```

---

### `EXPOSE`
- Indicates which **port** the container listens on.

```Dockerfile
EXPOSE 3000
```

---

### `USER`
- Sets the user to run the application.
- Avoid running as `root`.

```Dockerfile
RUN addgroup app && adduser -S -G app app
USER app
```

---

### `CMD`
- Defines the **default command** when starting a container.
- Only the **last CMD** is used if multiple are present.

```Dockerfile
CMD npm start                 # Shell form
CMD ["npm", "start"]         # Exec form
```

---

### `ENTRYPOINT`
- Similar to `CMD`, but **harder to override**.
- Use `--entrypoint` to override if needed.

```Dockerfile
ENTRYPOINT ["npm", "start"]
```

#### 🔄 CMD vs ENTRYPOINT

| Feature | CMD | ENTRYPOINT |
|--------|-----|-------------|
| Overridable | ✅ Easy | ⚠️ Needs `--entrypoint` |
| Purpose | Default command | Fixed command |
| Use Case | Run script with params | Run main app |

Examples:
```bash
docker run php-container sh             # Overrides CMD
docker run php-container php index.php  # Overrides CMD
docker run --entrypoint php php-container index.php  # Overrides ENTRYPOINT
```

---

## 📂 What is `.dockerignore`?

A file to **exclude** files/directories from the build context, similar to `.gitignore`.

---

## 🧱 What is a Container?

A **container** is a lightweight, isolated process with its own filesystem provided by the Docker image.

> ⚠️ **All data inside a container is ephemeral**. Use volumes for persistent storage.

---

## 💾 What is a Volume?

A **volume** is external storage (host directory or cloud) mounted into a container.

- **Survives container deletion**
- Best for **persistent data**

---

Let me know if you'd like a diagram or visual summary!
