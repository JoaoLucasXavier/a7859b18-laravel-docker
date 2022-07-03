# Start a laravel project with Mysql and Redis using docker

### Step 1

Clone this repository

```sh
git clone https://github.com/JoaoLucasXavier/a7859b18-laravel-docker.git
```

### Step 2

Create your laravel project in a7859b18-laravel-docker folder

```sh
curl -s https://laravel.build/sample | bash
```

### Step 3

Run docker

```sh
docker-compose up --build -d
```

### Step 4

Create `.env` file

```sh
cp .env.example .env
```

```sh
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=username
DB_PASSWORD=password
```

### Step 5

Run composer commands

```sh
docker-compose exec php composer install
```

```sh
docker-compose exec php php artisan key:generate
```

```sh
docker-compose exec php php artisan config:cache
```

### Step 6

Optional: Create a new MySQL user

```sh
docker-compose exec mysql bash
```

```sh
mysql -u root -p
```

```sh
GRANT ALL ON laravel.* TO 'new_user'@'%' IDENTIFIED BY 'your_user_password';
```

```sh
FLUSH PRIVILEGES;
```

```sh
EXIT;
```

### Step 7

Optional: Run migrations

```sh
docker-compose exec app php artisan migrate
```

```sh
docker-compose exec app php artisan tinker
```

```sh
\DB::table('migrations')->get();
```

### Step 8

Access your project
[http://localhost](http://localhost:80)
