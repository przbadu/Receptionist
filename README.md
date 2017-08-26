# Receptionist

A simple application in which `RESTful` apis are handled using asp.net core 2
and `Frontend` handled with react js.

## Setup Steps

1. Install [dotnet core](https://www.microsoft.com/net/core) in your platform. All three major platforms are supported.

2. Make sure everything is setup

I am running on `Mac os x`

```sh
➜  Receptionist git:(master) dotnet --info
.NET Command Line Tools (2.0.0)

Product Information:
 Version:            2.0.0
 Commit SHA-1 hash:  cdcd1928c9

Runtime Environment:
 OS Name:     Mac OS X
 OS Version:  10.12
 OS Platform: Darwin
 RID:         osx.10.12-x64
 Base Path:   /usr/local/share/dotnet/sdk/2.0.0/

Microsoft .NET Core Shared Framework Host

  Version  : 2.0.0
  Build    : e8b8861ac7faf042c87a5c2f9f2d04c98b69f28d
```

3. Now, we can start creating our application:

```sh
mkdir Receptionist && cd $_
dotnet new webapi # will create dotnet web api project
create-react-app client # will create react app inside client directory
```

4. Tweak the client build

For this we need to install 2 npm packages `rimram` to delete existing `wwwroot`
directory from dotnet app. And `ncp` to copy our react build directory inside it.

```sh
cd client
npm install --save-dev rimraf ncp # or use yarn
```

Open `client/package.json` file in your editor and add `postbuild`, `clean-server`,
and `copy-to-wwwroot` scripts:

```json
"scripts": {
  "start": "react-scripts start",
  "build": "react-scripts build",
  "postbuild": "npm run copy-to-wwwroot",
  "test": "react-scripts test --env=jsdom",
  "eject": "react-scripts eject",
  "clean-server": "rimraf server/wwwroot",
  "copy-to-wwwroot": "npm run clean-server && ncp ./build ../wwwroot"
}
```

5. Test our build script is working

```sh
npm run build
```

this script should remove your old build from wwwroot directory and copy your
`client/build` contents in it.
