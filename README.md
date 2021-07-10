# vue-whatsapp-widget

> WhatsApp chat widget for your website and your vue app
![Custom settings](https://i.ibb.co/FgR2NYS/widget-PNG.png.png)

## What is vue-whatsapp-widget?

This is a very simple floating WhatsApp button widget. In the current situation with the pandemic 2020 events, most of the small businesses have to move to online presence. A wey to short the communication with your customers is using a widget like this.

It adds a floating-like button to your site that calls the WhatsApp Chat API.

It will automatically begin a WhatsApp chat to the number that you configure and with the text that the user writes.

All texts are fully customizable.

## Install

```bash
npm install --save vue-whatsapp-widget
```

## Usage

```vue
<template>
    <vue-whatsapp-widget phoneNumber="+1111111111"/>
</template>
<script>
import VueWhatsappWidget from 'vue-whatsapp-widget'
components: {
    VueWhatsappWidget
}
</script>
```

⚠️ Where the `phoneNumber` is a full phone number in international format. Omit any zeroes, brackets, or dashes when adding the phone number in international format.

Example: `44222222` where 44 is the UK internacional code.

## Customization

| option        | value    | default                                   | description                                                                                                  |
| ------------- | -------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| phoneNumber   | `string` | `''`                                      | WhatsApp [intenational number](https://faq.whatsapp.com/en/general/21016748) which will receive the message. |
| textReply | `string` | `'Typically replies within an hour'`        |
| messages       | `array` | `'["Hi there 👋 How can I help you ?"]'` | With `\n` you can create a break-line.                                                                       |
| companyName   | `string` | `'Widget'`                               | Your company  name?                                                                                          |
| companyLogo    | `string` | `''`                                    | Your companyLogo                                                                                  |

## License

MIT
