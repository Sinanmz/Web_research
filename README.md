<div dir='rtl' align='justify'>
<p align="center"><img src="https://gobuffalo.io/images/logo.svg"/></p>
  
<p align="center">
    گردآوردندگان:  سینا نمازی، امیرحسین اکبری، محمد معین صمدی آزاد  
</p>
 


  # عناوین

- [Introduction](#introduction)

- [Overview](#overview)
  - [Backend Libraries](#backend-libraries)
  - [Frontend Libraries](#frontend-libraries)
 
- [Getting Started](#getting-started)
  - [Install Buffalo](#install-buffalo)
  - [Generating a New Project](#generating-a-new-project)
  - [Directory Structure](#directory-structure)


- [Building an API](#building-an-api)
  - [ُStarting a Buffalo Project](#Starting-a-buffalo-project)
  - [Database Setup](#database-setup)
  - [Migration](#migration)
  - [Creating our Model](#creating-our-model)
  - [Building our Actions](#building-our-actions)
  - [Creating the Routes](#creating-the-routes)
  - [Testing](#testing)
  
  
  
# Introduction
بوفالو یک ابزار قدرتمند برای توسعه برنامه ها‌ و وب سرویس های بزرگ و scalble است که برای زبان Golang توسعه داده شده است. نحوه طراحی بوفالو از چارچوب های دیگری مانند Ruby on rails و Django الهام گرفته شده که دید به اصطلاح convention over configuration را به توسعه وب دارد و توسعه وب اپلیکیشن های بسیار بزرگ را برای توسعه دهنده راحت تر می کند.

از جمله ویژگی های خوب بوفالو می توان به قالب بندی قانونمند پروژه، پیزوی از روش MVC (model-view-control)،داشتن قابلیت های middleware و routing قدرتمند، اداره asset ها و قابلیت های templating و همچنین ابزارهای جامع برای test اشاره کرد.





  # Overview
  در‌حالی که بوفالو ممکن است یک framework به حساب بیاید، اما به طور کلی بوفالو اکوسیستمی از کتاب خانه هایGo و Javascript بوده که در کنار‌ هم قرار گرفته اند و برای هماهنگی باهم انتخاب شده اند. بیشتر این اجزا می توانندبا ابزاری که عملکرد مشابه دارند جایگزین شوند، اما در حال حاضر این پیشفرض  توصیه می شود.

 در این بخش کمی به این آجر های سازنده پیشفرض یک buffalo app میپردازیم.

 ## Backend Libraries
 ### buffalo
 بوفالو مانند یک چسب در میان اجزا فراهم شده بوده و دور بقیه کتاب خانه ها و میپیچد و جریان کاری را مدیریت می کند.
 ### gorilla/mux
 gorilla mux یکی از پراستفاده ترین router ها در Go است. با اینکه بعضی از router ها مانند httprouter ازgorilla/mux سریع تر هستند، gorilla/mux قابلیت های بسیار بیشتری را داشته و به اندازی کافی سریع است.
 ### pop
pop، برای بوفالو ORM پیشفرض است. Soda toolbox را برای نیاز های مربوط به پایگاه داده را فراهم می کند وبسیاری از انواع دیتا بیس را پشتیبانی می کند مانند: PostgreSQL, MySQL, SQLite
(برای اطلاعات بیشتر درمورد کار های یک ORM می توانید به [اینجا](https://www.freecodecamp.org/news/what-is-an-orm-the-meaning-of-object-relational-mapping-database-tools/) مراجعه کنید)
 ### plush
 plush برای بوفالو templating engine پیشفرض بوده و سینتکس آن خیلی شبیه به ERB template ها در Ruby است.
(برای اطلاعات بیشتر درمورد کار های یک templating engin می توانید به [اینجا](https://www.educative.io/answers/what-are-template-engines) مراجعه کنید)

 ## Frontend Libraries
 ### Boostrap
 Boostrap یکی از معروف ترین کتابخانه های ابزار frontend است. این کتابخانه کمک می کند  interface ها را با بخش های معمول مثل جدول ها، carousel ها یا grid layout ها بسازیم.
### JQuery
JQuery یک کتابخانه غنی است که هدف آن این است که دستکاری کردن DOM  و فرستادن AJAX query ها را ساده کند. با این که امروزه کمتر استفاده می شود، اما بسیاری از پروژه ها هنوز آن را همراه دارند تا برای پشتیبانی از انواع مرورگر ها از آن کمک بگیرند.
### Webpack
Webpack یک Javascript assets bundler شناخته شده است . Webpack به صورت پیشفرض برای hash وکوچک کردن asset های شما تنظیم شده است.


# Publish/Subscribe
در پیش‌تر ما یک
work queue
ساختیم. در آنجا فرض این بود که هر پیام دقیقا به یک 
worker
می‌رود. در این بخش ماجرا کمی متفاوت است. ما می‌خواهیم که یک پیام را به چندین مصرف‌کننده ارسال کنیم. به این الگو
publish/subscribe
می‌گویند.

برای مشخص شدن ماجرا فرض کنید که می‌خواهیم یک سیستم مدیریت لاگ‌ها بسازیم.
این سیستم از دو برنامه تشکیل شده است.
برنامه‌ی اول پیام‌های لاگ تولید کرده و دیگری این پیام‌ها را دریافت کرده و آن‌ها را چاپ می‌کند.

در این سیستم هر کپی از برنامه‌ی دریافت کننده‌ای که اجرا شود پیام‌ها را دریافت خواهد کرد.
با این روش می‌توانیم یک دریافت‌کننده اجرا کنیم که پیام‌هایی که دریافت می‌کند را در دیست ذخیره کند و یک دریافت‌کننده‌ی دیگر نیز اجرا کنیم که لاگ‌ها را بر روی صفحه،نمایش  دهد.

در اصل ما پیام را به همه‌ی دریافت کننده‌ها
broadcast
می‌کنیم.

# Getting Started
## Install Buffalo
در این بخش یاد می گیرید چگونه Buffalo را نصب بکنید.

Buffalo در حال حاضر بر روی این پلتفرم ها تست شده و قابل نصی است:
- GNU/Linux
- Mac OSX
- Windows
### Requirements
قبل از نصب کردن مطمئن شوید پیشنیاز های مورد نیاز را نصب شده دارید:
- A working Go enviroment
- Go version v1.16.0
#### Frontend Requirements
نیازمندی های زیر اختیاری هستند، یعنی اگر بخواهید صرفا یک API بسازید یا برنامه خود را به شکل old-fashioned بسازید نیازی یه آن ها ندارید:
- node version 8 or greater
- either yarn or npm
#### Database Specific Requirements
اگر به دیتابیس نیازی ندارید نیز به این نیازمندی ها نیازی ندارید:
- SQLite3: GCC , r equivalent C compiler for mattn/gp-sqlite3
#### Installation
برای GNU/Linux دستورات زیر را وارد کنید:
  <div  dir='ltr'  align='justify'>

  ```bash
     wget https://github.com/gobuffalo/cli/releases/download/v0.18.14/buffalo_0.18.14_Linux_x86_64.tar.gz
     tar -xvzf buffalo_0.18.14_Linux_x86_64.tar.gz
     sudo mv buffalo /usr/local/bin/buffalo
  ```
  </div>
برای MacOS دستورات زیر را وارد کنید:
  <div  dir='ltr'  align='justify'>

  ```bash
     curl -OL https://github.com/gobuffalo/cli/releases/download/v0.18.14/buffalo_0.18.14_Darwin_x86_64.tar.gz
     tar -xvzf buffalo_0.18.14_Darwin_x86_64.tar.gz
     sudo mv buffalo /usr/local/bin/buffalo
     # or if you have ~/bin folder setup in the environment PATH variable
     mv buffalo ~/bin/buffalo
  ```
  </div>

  #### Verify Your Installation
  شما می توانید برای اطمینان از نصب شدن Buffalo دستور buffalo را در ترمینال خود اجرا کنید:
    <div  dir='ltr'  align='justify'>

  ```bash
     $ buffalo
Build Buffalo applications with ease

Usage:
  buffalo [command]

Available Commands:
  build       Build the application binary, including bundling of webpack assets
  completion  Generate the autocompletion script for the specified shell
  db          [PLUGIN] [DEPRECATED] please use `buffalo pop` instead.
  destroy     Destroy generated components
  dev         Run the Buffalo app in 'development' mode
  fix         Attempt to fix a Buffalo applications API to match version v0.18.6
  generate    Generate application components
  help        Help about any command
  info        Print diagnostic information (useful for debugging)
  new         Creates a new Buffalo application
  plugins     tools for working with buffalo plugins
  pop         [PLUGIN] A tasty treat for all your database needs
  routes      Print all defined routes
  setup       Setup a newly created, or recently checked out application.
  task        Run grift tasks
  test        Run the tests for the Buffalo app. Use --force-migrations to skip schema load.
  version     Print the version information

Flags:
  -h, --help   help for buffalo

Use "buffalo [command] --help" for more information about a command.
  ```
  </div>

  ## Generating a New Project
  حال که Buffalo را نصب کردید در این بخش یاد می گیرید چگونه یک web application جدید را از اول با استفاده از دستور buffalo شروع کنید.
  ### Create a New Project
  هدف Buffalo این است که ساختن یک web application از ابتدا را تا حد امکان ساده و سریع کند، و چه چیزی سریع تر و ساده تر از یک new application generator است؟
  در ابتدا به دایرکتوری که می خواهید پروژه شما در آن جا باشد بروید، سپس دستور زیر را اجرا کنید:
  <div  dir='ltr'  align='justify'>

  ```bash
     buffalo new project-name
  ```
  </div>
  اگر دستور شما به درستی کار کند با صحنه زیر مواجه می شوید:
  <div  dir='ltr'  align='justify'>

  ```bash
     $ buffalo new coke
DEBU[2022-05-25T11:06:33-05:00] Step: 435aea40
DEBU[2022-05-25T11:06:33-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:33-05:00] Exec: go mod init coke
go: creating new go.mod: module coke
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/README.md
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/actions/actions_test.go
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/actions/app.go
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/actions/home.go
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/actions/home_test.go
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/actions/render.go
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/cmd/app/main.go
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/.codeclimate.yml
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/.env
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/fixtures/sample.toml
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/grifts/init.go
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/inflections.json
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/config/buffalo-app.toml
DEBU[2022-05-25T11:06:33-05:00] Step: 638bde0d
DEBU[2022-05-25T11:06:33-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/Dockerfile
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/.dockerignore
DEBU[2022-05-25T11:06:33-05:00] Step: 7065092d
DEBU[2022-05-25T11:06:33-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/grifts/db.go
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/models/models.go
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/models/models_test.go
DEBU[2022-05-25T11:06:33-05:00] Step: 916dfca0
DEBU[2022-05-25T11:06:33-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/database.yml
DEBU[2022-05-25T11:06:33-05:00] Step: ff1c6d38
DEBU[2022-05-25T11:06:33-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:33-05:00] File: /your/path/coke/.buffalo.dev.yml
DEBU[2022-05-25T11:06:33-05:00] Step: 103396c6
DEBU[2022-05-25T11:06:33-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:33-05:00] Exec: go install github.com/gobuffalo/buffalo-pop/v3@latest
DEBU[2022-05-25T11:06:34-05:00] Step: ae1260b1
DEBU[2022-05-25T11:06:34-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/config/buffalo-plugins.toml
DEBU[2022-05-25T11:06:34-05:00] Step: 4992ff46
DEBU[2022-05-25T11:06:34-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/actions/app.go
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/actions/home.go
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/actions/home_test.go
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/actions/render.go
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/locales/all.en-us.yaml
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/locales/embed.go
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/public/embed.go
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/public/robots.txt
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/templates/_flash.plush.html
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/templates/application.plush.html
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/templates/embed.go
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/templates/home/index.plush.html
DEBU[2022-05-25T11:06:34-05:00] Step: 69d71878
DEBU[2022-05-25T11:06:34-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:34-05:00] LookPath: yarn
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/assets/css/_buffalo.scss
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/assets/css/application.scss
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/assets/images/favicon.ico
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/assets/images/logo.svg
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/assets/js/application.js
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/.babelrc
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/package.json
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/postcss.config.js
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/public/assets/keep
DEBU[2022-05-25T11:06:34-05:00] File: /your/path/coke/webpack.config.js
DEBU[2022-05-25T11:06:34-05:00] LookPath: yarn
DEBU[2022-05-25T11:06:34-05:00] Exec: yarn --version
1.22.17
DEBU[2022-05-25T11:06:34-05:00] Exec: yarn set version berry
➤ YN0000: Retrieving https://repo.yarnpkg.com/3.2.1/packages/yarnpkg-cli/bin/yarn.js
➤ YN0000: Saving the new release in .yarn/releases/yarn-3.2.1.cjs
➤ YN0000: Done in 0s 637ms
DEBU[2022-05-25T11:06:37-05:00] Exec: yarn config set enableGlobalCache true
➤ YN0000: Successfully set enableGlobalCache to true
DEBU[2022-05-25T11:06:37-05:00] Exec: yarn config set logFilters --json [{"code":"YN0013","level":"discard"}]
➤ YN0000: Successfully set logFilters to [
  {
    code: 'YN0013',
    text: undefined,
    pattern: undefined,
    level: 'discard'
  }
]
DEBU[2022-05-25T11:06:37-05:00] Exec: yarn --version
3.2.1
DEBU[2022-05-25T11:06:38-05:00] Exec: yarn install
DEBU[2022-05-25T11:06:38-05:00] ➤ YN0000: ┌ Resolution step

DEBU[2022-05-25T11:06:39-05:00] ➤ YN0032: │ fsevents@npm:2.3.2: Implicit dependencies on node-gyp are discouraged

DEBU[2022-05-25T11:06:43-05:00] ➤ YN0000: └ Completed in 5s 401ms

DEBU[2022-05-25T11:06:43-05:00] ➤ YN0000: ┌ Fetch step

DEBU[2022-05-25T11:06:43-05:00] ➤ YN0000: └ Completed

DEBU[2022-05-25T11:06:43-05:00] ➤ YN0000: ┌ Link step

DEBU[2022-05-25T11:06:44-05:00] ➤ YN0000: │ ESM support for PnP uses the experimental loader API and is therefore experimental

DEBU[2022-05-25T11:06:44-05:00] ➤ YN0007: │ @fortawesome/fontawesome-free@npm:5.15.4 must be built because it never has been before or the last one failed

DEBU[2022-05-25T11:06:44-05:00] ➤ YN0000: └ Completed in 0s 906ms

DEBU[2022-05-25T11:06:44-05:00] ➤ YN0000: Done with warnings in 6s 462ms

DEBU[2022-05-25T11:06:44-05:00] Step: bb3c28ed
DEBU[2022-05-25T11:06:44-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:44-05:00] Exec: go mod tidy
go: finding module for package github.com/gobuffalo/buffalo
go: finding module for package github.com/gobuffalo/mw-paramlogger
go: finding module for package github.com/gobuffalo/buffalo-pop/v3/pop/popmw
go: finding module for package github.com/gobuffalo/mw-i18n/v2
go: finding module for package github.com/gobuffalo/buffalo/render
go: finding module for package github.com/gobuffalo/mw-forcessl
go: finding module for package github.com/gobuffalo/envy
go: finding module for package github.com/gobuffalo/mw-csrf
go: finding module for package github.com/unrolled/secure
go: finding module for package github.com/markbates/grift/grift
go: finding module for package github.com/gobuffalo/pop/v6
go: finding module for package github.com/gobuffalo/suite/v4
go: found github.com/gobuffalo/buffalo in github.com/gobuffalo/buffalo v0.18.7
go: found github.com/gobuffalo/buffalo-pop/v3/pop/popmw in github.com/gobuffalo/buffalo-pop/v3 v3.0.4
go: found github.com/gobuffalo/buffalo/render in github.com/gobuffalo/buffalo v0.18.7
go: found github.com/gobuffalo/envy in github.com/gobuffalo/envy v1.10.1
go: found github.com/gobuffalo/mw-csrf in github.com/gobuffalo/mw-csrf v1.0.0
go: found github.com/gobuffalo/mw-forcessl in github.com/gobuffalo/mw-forcessl v0.0.0-20220514125302-be60179938a4
go: found github.com/gobuffalo/mw-i18n/v2 in github.com/gobuffalo/mw-i18n/v2 v2.0.1
go: found github.com/gobuffalo/mw-paramlogger in github.com/gobuffalo/mw-paramlogger v1.0.0
go: found github.com/unrolled/secure in github.com/unrolled/secure v1.10.0
go: found github.com/markbates/grift/grift in github.com/markbates/grift v1.5.0
go: found github.com/gobuffalo/pop/v6 in github.com/gobuffalo/pop/v6 v6.0.4
go: found github.com/gobuffalo/suite/v4 in github.com/gobuffalo/suite/v4 v4.0.2
DEBU[2022-05-25T11:06:45-05:00] Exec: go mod download
DEBU[2022-05-25T11:06:46-05:00] Step: 218a906c
DEBU[2022-05-25T11:06:46-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:46-05:00] Step: a3cee09e
DEBU[2022-05-25T11:06:46-05:00] Chdir: /your/path/coke
DEBU[2022-05-25T11:06:46-05:00] File: /your/path/coke/.gitignore
DEBU[2022-05-25T11:06:46-05:00] Exec: git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint: 	git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint: 	git branch -m <name>
Initialized empty Git repository in /your/path/coke/.git/
DEBU[2022-05-25T11:06:46-05:00] Exec: git add .
DEBU[2022-05-25T11:06:46-05:00] Exec: git commit -q -m Initial Commit
INFO[2022-05-25T11:06:46-05:00] Congratulations! Your application, coke, has been successfully generated!
INFO[2022-05-25T11:06:46-05:00] You can find your new application at: /your/path/coke
INFO[2022-05-25T11:06:46-05:00] Please read the README.md file in your new application for next steps on running your application.
  ```
  </div>
  با اجرای این دستور یک Buffalo application به نام project-name در دایرکتوری شما ساخته می شود از جمله مواردی که این دستور اضافه می کند می توان به موارد زیر اشاره کرد:

  - همه Go depenedency های مورد نیاز
  - شروع کردن یک Git repository
  - Frontend dependency های مورد نیاز

  ### Create a Customized App
  default setup ای که Buffalo انتخاب می کند خیلی خوب است اما ممکن است شما بخواهید آن را به شکلی که دوست دارید تغییر بدهید، برای مثال از دیتابیس mariadb به جای postgres استفاده بکنید. برای این نوع کار ها از دستور زیر استفاده کنید تا لیست flag های مورد نیاز برای این کار را ببینید:
  <div  dir='ltr'  align='justify'>

  ```bash
     $ buffalo help new
    Creates a new Buffalo application

    Usage:
    buffalo new [name] [flags]

    Flags:
          --api                  skip all front-end code and configure for an API server
          --ci-provider string   specify the type of ci file you would like buffalo to generate [none, travis, gitlab-ci, circleci] (default "none")
        --config string        config file (default is $HOME/.buffalo.yaml)
        --db-type string       specify the type of database you want to use [cockroach, mariadb, mysql, postgres, sqlite3] (default "postgres")
     -d, --dry-run              dry run
     -f, --force                delete and remake if the app already exists
     -h, --help                 help for new
          --module string        specify the root module (package) name. [defaults to 'automatic']
         --skip-config          skips using the config file
         --skip-docker          skips generating the Dockerfile
          --skip-pop             skips adding pop/soda to your app
          --skip-webpack         skips adding Webpack to your app
          --skip-yarn            use npm instead of yarn for frontend dependencies management
          --vcs string           specify the Version control system you would like to use [none, git, bzr] (default "git")
    -v, --verbose              verbosely print out the go get commands
  ```
  </div>
  همانطور که می بینی می توانین انتخاب کنید که یک API application ایجاد کنید و کلا بخش های Front end را skip کنید و ...

  ### Override Default Config
  در حالت عادی دستور buffalo new به دنبال یک confiratio file در آدرس $HOME/ .buffalo.yml می گردد و اگر وجود داشت تلاش می کند طبق آن عمل کند. شما می توانید با استفاده از flag ها آن را override  کنید و آن های که دوست دارید را پاس بدهید و یا با استفاده از --config آدرس یک فایل YAML دیگری را بدهید. همچنین استفاده از --skip-config باعث می شود که هر فایل  config را نادیده بگیرد و فقط بر اساس flag هایی که داده می شود عمل کند.
  
  یک نمونه از فایل config به شکل زیر است:

  <div  dir='ltr'  align='justify'>

  ```yaml
    skip-yarn: true
    db-type: postgres
    bootstrap: 4
    with-dep: true
  ```
  </div>

  ### Running Your Application in Development
  یکی از بدی های GO development  این است که اگر تغییری در برنامه خود بدهیم نیاز است اپلیکیشن خود را متوقف کنیم و دوباره آن را راه بیاندازیم تا تغییرات را ببینیم. اما در Buffalo کافیست دسور زیر را اجرا کنیم:
  <div  dir='ltr'  align='justify'>

  ```bash
    buffalo dev
  ```
  </div>
  ای دستور فایل های .go و .html و فولدر asset را زیر نظر می گیرد و هرگاه تغییری در آن بدهید آن را نشان می دهد.
  کافیست این دستور را اجرا کنیو و به localhost:3000 برویم تا تغییرات را ببینیم.
  
  #### Run the dev server on a custom port
  گاهی پورت 3000 در دستگاه شما مشغول است و باید برنامه را بر روی پورت دیگری اجرا کنید، این کار با دستور زیر انجام می شود:
  <div  dir='ltr'  align='justify'>

  ```bash
    PORT=3001 buffalo dev
  ```
  </div>

   ## Directory Structure
Buffalo یک ساختار directory مینیمال را برای شما فراهم می کند تا بتوانید روی پروژه کار بکنید. این ساختار به تمیز نگه داشتن پروژه شما کمک می کند و به عملکرد بهتر generator ها کمک می کند. 

حال با ساختار یک پروژه Buffalo آشنا می شویم.

### The Root Directory
 نمودار زیر ساختار یک پروژه Buffalo را نشان می دهد:

 <div  dir='ltr'  align='justify'>

  ```
├── .yarn/
├── actions/
│	├── app.go
│	└── render.go
├── assets/
├── cmd/
│	└── app/
│		└── main.go
├── config/
├── fixtures/
├── grifts/
├── models/
├── public/
├── templates/
├── .babelrc
├── .buffalo.dev.yml
├── .codeclimate.yml
├── .docketignore
├── .env
├── .gitignore
├── .pnp.loader.mjs
├── .yarnrc.yml
├── database.yml
├── Dockerfile
├── go.mod
├── go.sum
├── inflections.json
├── package.json
├── postcss.config.js
├── README.md
├── webpack.config.js
└── yarn.lock
  ```
  </div>

### actions
در این دایرکتوری بخش Controller  طراحی MVC قرار می گیرد. این دایرکتوری شامل handler ها برای URL است. به علاوه شامل 2 فایل زیر نیز است:
- app.go که کار برپا کردن برنامه و reouteها را انجام می دهد
- render.go که کار برپا کردن templage engineها را انجام می دهد.
### assets
این دایرکتوری شامل فایل های خام asset است که این فایل ها کامپایل شده و سپس به دایرکتوری public می شند که به آم خواهیم پرداخت.
(این دایرکتوری اجباری نیست برای مثال اگر می خواهیم یک API بنویسیم که فاقد frontend است، می تواند پاک شود.)
### cmd
این دایرکتوری شامل فایل main.go است که کار از ایتدا شروع کردن برنامه یا به اصطلاح bootstrap کردن آن را انجام می دهد.

### grifts
این دایرکتوری شامل task ها است که با کتابخانه grift کنترل می شوند.
(taskها اسکریپت های کوتاهی هستند معمولا برای راه اندازی یک اپلیکیشن نیاز می شوند. کار هایی که این اسکریپت ها می کنند می تواند database seeding, پارس کردن log file باشد. Buffalo از کتابخانه grift برای آسان کردن نوشتن این اسکریپت ها استفاده می کند.)
(این دایرکتوری اجباری نیست. اگر از task ها استفاده ای نمی کنیم می تواند پاک شود.)

### models
در این دایرکتوری بخش Model از طراحی MVC قرار می گیرد. این دایرکتوری شامل فایل models.go است که وضیفه initialize کردن ارتباط با datasource را انجام می دهد.
(اگر از generator های pop/soda برای generate کردن مدل ها استفاده می کنید در این جا generate می شوند.)
  (این دایرکتوری نیز اختیاری است و اگر از دیتابیس استفاده نمی کنید می تواند پاک شود.)

### public
این دایرکتوری شامل asset های کامپایل شده است و اگر از webpack استفاده می کنید، asset های خود را در اینجا قرار می دهد.
(محتوای این دایرکتوری به شکل auto-generated هستند.)  
  
  ### templates
  در این دایرکتوری بخش View در طراحی MVC قرار می گیرد. در این دایرکتوری template ها (برای مثال فایل های HTML قرار می گیرند.)
  (این دایرکتوری اجباری نیست برای مثال اگر می خواهیم یک API بنویسیم که فاقد frontend است، می تواند پاک شود.)
  
  ### tmp
  این دایرکتوری توسط دستور Buffalo dev استفاده شده و برای دوباره ساختن پروژه هنگام هر تغییر است.
  (محتوای این دایرکتوری به شکل auto-generated هستند.) 

  ### database.yml
   این دایرکتوری شامل database configuration برای soda/pop است.
   (این دایرکتوری نیز اختیاری است و اگر از دیتابیس استفاده نمی کنید می تواند پاک شود.)
  
  


  # Building an API
  در این بخش قصد داریم برای آشنایی بیشتر با Buffalo به صورت عملی، یک API ساده بنویسیم. این API کار هایی باید در طول روز انجام دهیم را دریافت کرده و آن ها را در یک دیتابیس ذخیره کرده و به طور کلی یک TODO List درست می کند. در این مسیر با بخش های مختلف یک Buffalo project آشنا می شویم و نحوه ارتباط آن  با دیتابیس را بررسی می کنیم و نقش Migration را متوجه می شویم.

## Starting a Buffalo Project
شروع کردن یک Buffalo project با استفاده از دستور buffalo new انجام می شود. در این جا جون قصد داریم یک API بسازیم به آن --api را اضافه می کنیم.
حال دستور را اضافه می کنیم:

<div  dir='ltr'  align='justify'>

  ```bash
  sina@sina-Zephyrus-S-GX531GS-GX531GS:~$ buffalo new project --api
DEBU[2023-06-25T00:56:12+03:30] Step: 93e62b4e
DEBU[2023-06-25T00:56:12+03:30] Chdir: /home/sina/project
DEBU[2023-06-25T00:56:12+03:30] Exec: go mod init project
go: creating new go.mod: module project
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/README.md
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/actions/actions_test.go
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/actions/app.go
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/actions/home.go
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/actions/home_test.go
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/actions/render.go
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/cmd/app/main.go
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/.codeclimate.yml
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/.env
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/fixtures/sample.toml
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/grifts/init.go
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/inflections.json
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/config/buffalo-app.toml
DEBU[2023-06-25T00:56:12+03:30] Step: 84d01f8a
DEBU[2023-06-25T00:56:12+03:30] Chdir: /home/sina/project
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/Dockerfile
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/.dockerignore
DEBU[2023-06-25T00:56:12+03:30] Step: 993376dd
DEBU[2023-06-25T00:56:12+03:30] Chdir: /home/sina/project
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/grifts/db.go
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/models/models.go
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/models/models_test.go
DEBU[2023-06-25T00:56:12+03:30] Step: 4accb71e
DEBU[2023-06-25T00:56:12+03:30] Chdir: /home/sina/project
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/database.yml
DEBU[2023-06-25T00:56:12+03:30] Step: dca0f905
DEBU[2023-06-25T00:56:12+03:30] Chdir: /home/sina/project
DEBU[2023-06-25T00:56:12+03:30] File: /home/sina/project/.buffalo.dev.yml
DEBU[2023-06-25T00:56:12+03:30] Step: 03f3dc0d
DEBU[2023-06-25T00:56:12+03:30] Chdir: /home/sina/project
DEBU[2023-06-25T00:56:12+03:30] Exec: go install github.com/gobuffalo/buffalo-pop/v3@latest
DEBU[2023-06-25T00:56:13+03:30] Step: a97717d1
DEBU[2023-06-25T00:56:13+03:30] Chdir: /home/sina/project
DEBU[2023-06-25T00:56:13+03:30] File: /home/sina/project/config/buffalo-plugins.toml
DEBU[2023-06-25T00:56:13+03:30] Step: 5e64f597
DEBU[2023-06-25T00:56:13+03:30] Chdir: /home/sina/project
DEBU[2023-06-25T00:56:13+03:30] File: /home/sina/project/actions/app.go
DEBU[2023-06-25T00:56:13+03:30] File: /home/sina/project/actions/home.go
DEBU[2023-06-25T00:56:13+03:30] File: /home/sina/project/actions/home_test.go
DEBU[2023-06-25T00:56:13+03:30] File: /home/sina/project/actions/render.go
DEBU[2023-06-25T00:56:13+03:30] File: /home/sina/project/locales/all.en-us.yaml
DEBU[2023-06-25T00:56:13+03:30] File: /home/sina/project/locales/embed.go
DEBU[2023-06-25T00:56:13+03:30] Step: 54b17c72
DEBU[2023-06-25T00:56:13+03:30] Chdir: /home/sina/project
DEBU[2023-06-25T00:56:13+03:30] Exec: go mod tidy
go: finding module for package github.com/gobuffalo/buffalo
go: finding module for package github.com/gobuffalo/grift/grift
go: finding module for package github.com/gobuffalo/buffalo/render
go: finding module for package github.com/gobuffalo/buffalo-pop/v3/pop/popmw
go: finding module for package github.com/gobuffalo/middleware/i18n
go: finding module for package github.com/gobuffalo/middleware/paramlogger
go: finding module for package github.com/gobuffalo/middleware/forcessl
go: finding module for package github.com/rs/cors
go: finding module for package github.com/gobuffalo/middleware/contenttype
go: finding module for package github.com/gobuffalo/envy
go: finding module for package github.com/unrolled/secure
go: finding module for package github.com/gobuffalo/x/sessions
go: finding module for package github.com/gobuffalo/pop/v6
go: finding module for package github.com/gobuffalo/suite/v4
go: found github.com/gobuffalo/buffalo in github.com/gobuffalo/buffalo v1.1.0
go: found github.com/gobuffalo/buffalo-pop/v3/pop/popmw in github.com/gobuffalo/buffalo-pop/v3 v3.0.7
go: found github.com/gobuffalo/buffalo/render in github.com/gobuffalo/buffalo v1.1.0
go: found github.com/gobuffalo/envy in github.com/gobuffalo/envy v1.10.2
go: found github.com/gobuffalo/middleware/contenttype in github.com/gobuffalo/middleware v1.0.0
go: found github.com/gobuffalo/middleware/forcessl in github.com/gobuffalo/middleware v1.0.0
go: found github.com/gobuffalo/middleware/i18n in github.com/gobuffalo/middleware v1.0.0
go: found github.com/gobuffalo/middleware/paramlogger in github.com/gobuffalo/middleware v1.0.0
go: found github.com/gobuffalo/x/sessions in github.com/gobuffalo/x v0.1.0
go: found github.com/rs/cors in github.com/rs/cors v1.9.0
go: found github.com/unrolled/secure in github.com/unrolled/secure v1.13.0
go: found github.com/gobuffalo/grift/grift in github.com/gobuffalo/grift v1.5.2
go: found github.com/gobuffalo/pop/v6 in github.com/gobuffalo/pop/v6 v6.1.1
go: found github.com/gobuffalo/suite/v4 in github.com/gobuffalo/suite/v4 v4.0.4
DEBU[2023-06-25T00:56:20+03:30] Exec: go mod download
DEBU[2023-06-25T00:56:20+03:30] Step: ae497430
DEBU[2023-06-25T00:56:20+03:30] Chdir: /home/sina/project
DEBU[2023-06-25T00:56:20+03:30] Step: fde62f00
DEBU[2023-06-25T00:56:20+03:30] Chdir: /home/sina/project
DEBU[2023-06-25T00:56:20+03:30] File: /home/sina/project/.gitignore
DEBU[2023-06-25T00:56:20+03:30] Exec: git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint: 	git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
Initialized empty Git repository in /home/sina/project/.git/
DEBU[2023-06-25T00:56:20+03:30] Exec: git add .
DEBU[2023-06-25T00:56:20+03:30] Exec: git commit -q -m Initial Commit
INFO[2023-06-25T00:56:20+03:30] Congratulations! Your application, project, has been successfully generated!
INFO[2023-06-25T00:56:20+03:30] You can find your new application at: /home/sina/project
INFO[2023-06-25T00:56:20+03:30] Please read the README.md file in your new application for next steps on running your application.

  ```
  </div>
  اضافه کردن این flag باعث می شود ساختار پروژه ما متفاوت باشد، برای مثال بخش های مربوط به frontend در آن نباشد.
  حال با cd کردن به دایرکتوری پروژه می توانیم موارد اضافه شده را ببینیم:

 ![dsa]("C:\Users\sinan\Desktop\buffalo\structure.png")  

## Database Setup
در ابتدا باید دیتابیس خود را آماده کنیم. اینجا حق انتخاب بین انواع دیتابیس را داریم اما من دیتابیس Postgres را به دلیل آشنایی بیشتر با آن انتخاب کردم.
برای راه اندازی  Postgres از Docker استفاده می کنیم. برای این هدف،  یک Dockerfile به شکل زیر می نویسیم:
<div  dir='ltr'  align='justify'>

  ```dockerfile
FROM postgres:latest

ENV POSTGRES_USER test
ENV POSTGRES_PASSWORD test

COPY init.sql /docker-entrypoint-initdb.d/

EXPOSE 5432
  ```
  </div>
 این داکر فایل ابتدا از یک Postgres image شروع کرده و یک user به نام test در آن میسازد که Password آن نیز test است. همچنین فایل init.sql که در همان دایرکتوری قرار دارد را به این image منتقل کرده و محتویان آن اجرا می شود.
 
 
  فایل init.sql:
  <div  dir='ltr'  align='justify'>

  ```sql
CREATE DATABASE project_development;

GRANT ALL PRIVILEGES ON DATABASE project_development TO test;
  ```
  </div>
با اجرا شدن این فایل یک دیتابیس به نام project_development ساخته شده و به User ما تمام دسترسی ها را در مورد این دیتابیس می دهد.



















- [Building an API](#building-an-api)
  - [Database Setup](#database-setup)
  - [Migration](#migration)
  - [Creating our Model](#creating-our-model)
  - [Building our Actions](#building-our-actions)
  - [Creating the Routes](#creating-the-routes)
  - [Testing](#testing)
