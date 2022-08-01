# How to create a PHP laravel project

## 1. Install composor
Google `how to install php composor on xx`.

## 2. Install laravel
```bash
composer global require laravel/installer
```

## 3. Create a new project
```bash
composer create-project laravel/laravel new_app

cd new_app
```

## 4. Turn it into a vite-vue project
```bash
composer require laravel/breeze --dev

php artisan breeze:install vue --ssr
```

## 5. Run it
```bash
npm install

php artisan serve

# open another terminal
npm run dev
```

> I don't know your's. But for me, this is not working.