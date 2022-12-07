# OTP UI

This project is about OTP UI.
You can customize OTP length, form title and description.

## Project Prerequisite

1. Angular CLI v13.0.0
2. Node.js v16.16.0
3. Project uses [ngx-bootstrap](https://www.npmjs.com/package/ngx-bootstrap) v8.0.0, To add ngx-bootstrap : <br /> `ng add ngx-bootstrap@8.0.0`

## Running Development server

1. `npm i` in root directory
2. `ng serve` for dev server (`http://localhost:4200/`)

## Running unit tests

1. Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Adding Component to your project

- Copy OTP module to your project
- Add OtpModule to your module

```

@NgModule({
  ...
  imports: [
    ...
    OtpModule,
    ...
  ],
  ...
})
```

- Implementation - 1 : Show using HTML template

```
// in html file:
...
<otp-component *ngIf="show" (onVerify)="verify($event)"></otp-component>
...

// in ts file:
...
show=true;
verify(otp:number){
  console.log(otp)
}
...
```

- Implementation - 2 : Show using OtpService.

```
import { OtpService } from './otp/services/otp.service';
...
constructor(private otpService: OtpService) {
  this.otpService.onVerify.subscribe((otp) => {
    console.log(otp);
  });
}
...
// Show the otp form
this.otpService.show({
  formMessage: 'this is form message',
  formTitle: 'First',
  otpLength: 6,
});

// Manually hide the otp form
this.otpService.hide();
```

## Documentation

See appComponent for example.

### OtpService.show({params})

&nbsp;&nbsp;Display OTP form compoent to UI with given params.
| Params | Type | Default | Description |
| ----------- | ------ | ------------------------------------------- | ------------------------------------------------------------------------- |
| formTitle | string | OTP Verification | Display title of the form. |
| formMessage | string | Please enter the OTP that we have sent you. | Display message in small font. for ex. (we have sent mail to xyz@abc.com) |
| otpLength | number | 4 | Length Of OTP |

### OtpService.hide()

&nbsp;&nbsp; To manually hide OTP component from UI, no params reqired.

### OtpService.onVerify

&nbsp;&nbsp; You can subscribe to this Observable. <br />
&nbsp;&nbsp; It will be called when user press verify button with OTP as a value. <br />
&nbsp;&nbsp; Example:
&nbsp;&nbsp;

```
this.otpService.onVerify.subscribe((otp) => {
  console.log(otp);
});
```
