# Kavenegar nest module

kavenegar api for nestjs.

## Installation:


``` npm i @webafra/kavenegar-nestjs```

## Usage:

Import **kavenegarModule** inside your module:

```
// inside SmsModule*.module.ts

import { KavenegarModule } from "@webafra/kavenegar-nestjs"

@Module({
  imports:[
    KavenegarModule.forRoot({
      apikey:"your kavenegar apiKey"
    })
  ],
  controllers: [SmsController],
  providers: [SmsService]
})
export class SmsModule {}
```

Inject **KavenegarService** into your service: 


```
// inside SmsService*.service.ts

import { KavenegarService } from "@webafra/kavenegar-nestjs";

// example message types based on http://kavenegar.com/rest.html
export interface sendMessage {
    message: string;
    sender: string;
    receptor: string;
}
export interface verifyLookUpMessage {
    template: string;
    token: string;
    receptor: string;
}

@Injectable()
export class SmsService {
    constructor(private readonly sender: KavenegarService) {}
    sendMessage(data: sendMessage ){
        return this.sender.Send(data)
    }
    verifyLookUp(data: verifyLookUpMessage ){
        return this.sender.verifyLookUp(data)
    }
}
```


all of the methods are promised.
