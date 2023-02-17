# Learn NestJS

## Installing NestJS CLI

```
npm i -g @nestjs/cli
```

## Creating project

```
nest new project-name
```

If you are working with windows machine and newly installed cli is unable to get executed then we will force execute it with `npx`

```
npx nest new project-name
```

## NestJS Project Flow

NestJS follows the MVC structure like other frameworks for example Ruby on Rails, Django, etc. The project structure basically consists of 4 major layers.<br>
1. Modules: Deals with the complete structure of the particular service that you are creating.
2. Interfaces: Deals with the models. Used to create database structure.
3. Services: This handles business logics.
4. Controllers: This handles the request from the client and send the proper response. We usually link this with the working methods defined inside the Services.

## Example Project: IPL Table
We are going to create APIs to fetch data of players participated in IPL. For this project, we are not going to configure the databases but instead will define the data in the JSON format explicitly.<br>

List of APIs that we are going to create:
1. `GET /players`: Fetch player data
2. `GET /teams`: Fetch team data
3. `POST /players`: Send player data

### Creating the project
```
npx nest new ipl-proj
```

### Creating a complete Players route

#### Creating a module Players
```
npx nest generate module players
```
This will create a folder called as `players` inside which a file called as `players.module.ts` has been created.

#### Creating a interface Players

```
npx nest generate interface players
```
This will create a file called as `players.interface.ts` inside the `players` folder.

#### Creating a service Players
```
npx nest generate service players
```

#### Creating a controller Players

```
npx nest generate controller players
```

### Writing some logic and creating routes
Step 1: We will write now business logic inside the `players.service.ts` file. This is how my `players.service.ts` is looking like.
```
import { Injectable } from '@nestjs/common';

@Injectable()
export class PlayersService {
    getPlayerName(): object{
        return [{
            "id":1,
            "playerName": "Virat Kohli",
            "type": "batsman"
        },
        {
            "id":2,
            "playerName": "Rohit Sharma",
            "type": "batsman"
        },
        {
            "id":3,
            "playerName": "Ashwin",
            "type": "bowler"
        }
    ]
    }
}

```

Let's use this service inside the controllers which is `players.controller.ts`.

```
import { Controller, Get } from '@nestjs/common';
import { PlayersService } from './players.service';

@Controller('players')
export class PlayersController {
    constructor(private readonly playerService:PlayersService){}

    @Get()
    getPlayerName(): object{
        return this.playerService.getPlayerName()
    }
    
}
```

All the modules need to be registered inside the App module. By default it automatically gets registered.
```
imports: [PlayersModule]
```
