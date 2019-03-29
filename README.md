## vue-slider

A simple slider component for Vue2.x

### Installation

    npm install vue-slider

### Usage

    import Slider from 'vue-slider'

    <template>
      <Slider :images="[]" :interval="3000"></Slider>
    </template>

### Options

|    Name    | Type | Default | Description
| :--------: | :--: | :-----: | :--: |
| images     |  {Array}  |  | image url
| interval       |  {Number}  | 4000 | interval of the auto loop

### Demo

#### Auto play

![auto play](./doc/gif1.gif)

#### Support gesture switching

![Support gesture switching](./doc/gif2.gif)