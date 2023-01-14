<template>
  <h1 @click="drags = true">Устройство</h1>
  <table>
    <tbody>
      <tr>
        <td>Платформа:</td>
        <td>{{ navigator.userAgentData.platform }}</td>
      </tr>
      <tr>
        <td>Устройство мобильное</td>
        <td>{{ navigator.userAgentData.mobile }}</td>
      </tr>
      <tr>
        <td>Количество ядер CPU:</td>
        <td>{{ navigator.hardwareConcurrency }}</td>
      </tr>
      <tr>
        <td>Количество оперативной памяти ОЗУ:</td>
        <td>{{ navigator.deviceMemory }} Гб</td>
      </tr>
      <tr>
        <td>Поддерживаемое максимальное количество одновременно нажатых точек на экране:</td>
        <td>{{ navigator.maxTouchPoints }}</td>
      </tr>
      <tr>
        <td>Уровень заряда батареи:</td>
        <td>{{ Math.floor(batteryLevel) }}%</td>
      </tr>
      <tr>
        <td>Примерное время до разряда:</td>
        <td>{{ Math.floor(batteryTimeRemaining / 3600) }} часов {{ ('0' + Math.floor((batteryTimeRemaining % 3600) /
        60)).slice(-2) }} минут</td>
      </tr>
      <tr>
        <td>Подключена ли зарядка:</td>
        <td>{{ batteryCharging }}</td>
      </tr>
      <!-- <tr>
        <td>Содержимое буфера обмена:</td>
        <td>{{ clipboard }}</td>
      </tr> -->
    </tbody>
  </table>
  <h1>Экран</h1>
  <table>
    <tbody>
      <tr>
        <td>Разрешение экрана</td>
        <td>
          {{ Math.round(screen.width * window.devicePixelRatio) }}
          х
          {{ Math.round(screen.height * window.devicePixelRatio) }}</td>
      </tr>
      <tr>
        <td>Разрешение в браузере</td>
        <td>{{ screen.width }} х {{ screen.height }}</td>
      </tr>
      <tr>
        <td>Кратность масштабирования интерфейса</td>
        <td>{{ window.devicePixelRatio }} x</td>
      </tr>
      <tr>
        <td>Глубина цвета</td>
        <td>{{ screen.colorDepth }} бит</td>
      </tr>
      <tr>
        <td>Битовая глубина экрана</td>
        <td>{{ screen.pixelDepth }}</td>
      </tr>
      <tr>
        <td>Ориентация</td>
        <td>{{ screen.orientation.type }}</td>
      </tr>
      <tr>
        <td>Является дополнительным</td>
        <td>{{ screen.isExtended }}</td>
      </tr>
    </tbody>
  </table>
  <h1>Браузер:</h1>
  <table>
    <tbody>
      <tr>
        <td>Версия браузера</td>
        <td>{{ navigator.appVersion }}</td>
      </tr>
      <tr>
        <td>Имя поставщика браузера</td>
        <td>{{ navigator.vendor }}</td>
      </tr>
      <tr>
        <td>Включены ли cookie в браузере</td>
        <td>{{ navigator.cookieEnabled }}</td>
      </tr>
      <tr>
        <td>Язык интерфейса браузера</td>
        <td>{{ navigator.language }}</td>
      </tr>
      <tr>
        <td>Сайт из которого сюда попали</td>
        <td>{{ document?.referrer }}</td>
      </tr>
      <tr>
        <td>Количество страниц в истории данной вкладки</td>
        <td>{{ window.history.length }}</td>
      </tr>
    </tbody>
  </table>
  <h1>Сеть</h1>
  <table>
    <tbody>
      <tr>
        <td>Тип подключения к сети</td>
        <td>{{ connection.effectiveType }}</td>
      </tr>
      <tr>
        <td>Максимальная скорость</td>
        <td>{{ connection.downlink }} Мбит</td>
      </tr>
      <tr>
        <td>Скорость ответа сети (rtt)</td>
        <td>{{ connection.rtt }} мс</td>
      </tr>
      <tr>
        <td>Режим экономии данных в браузере</td>
        <td>{{ connection.saveData }}</td>
      </tr>
      <tr>
        <td>Type</td>
        <td>{{ connection.type }}</td>
      </tr>
    </tbody>
  </table>
  <h1 v-if="ipData">IP</h1>
  <table v-if="ipData">
    <tbody>
      <tr>
        <td>IP адресс</td>
        <td>{{ ipData.ipAddress }}</td>
      </tr>
      <tr>
        <td>Континент</td>
        <td>{{ ipData.continentName }}, {{ ipData.continentCode }}</td>
      </tr>
      <tr>
        <td>Страна</td>
        <td>{{ ipData.countryName }}, {{ ipData.countryCode }}</td>
      </tr>
      <tr>
        <td>Область</td>
        <td>{{ ipData.stateProv }}</td>
      </tr>
      <tr>
        <td>Город</td>
        <td>{{ ipData.city }}</td>
      </tr>
    </tbody>
  </table>
  <h1 v-if="position">Геолокация</h1>
  <table v-if="position">
    <tbody>
      <tr>
        <td>Широта</td>
        <td>{{ position.coords.latitude }}</td>
      </tr>
      <tr>
        <td>Долгота</td>
        <td>{{ position.coords.longitude }}</td>
      </tr>
      <tr>
        <td>Высота</td>
        <td>{{ position.coords.altitude }}</td>
      </tr>
      <tr>
        <td>Точность</td>
        <td>{{ position.coords.accuracy }}</td>
      </tr>
      <tr>
        <td>Точность высоты</td>
        <td>{{ position.coords.altitudeAccuracy }}</td>
      </tr>
      <tr>
        <td>Скорость</td>
        <td>{{ position.coords.speed }}</td>
      </tr>
      <tr>
        <td>Заголовок</td>
        <td>{{ position.coords.heading }}</td>
      </tr>
    </tbody>
  </table>
  <h1>Акселерометр</h1>
  <table>
    <tbody>
      <tr>
        <td>Координата x</td>
        <td>{{ x?.toFixed(2) }}</td>
      </tr>
      <tr>
        <td>Координата y</td>
        <td>{{ y?.toFixed(2) }}</td>
      </tr>
      <tr>
        <td>Координата z</td>
        <td>{{ z?.toFixed(2) }}</td>
      </tr>
    </tbody>
  </table>
  <h1>Device Orientation Event</h1>
  <table>
    <tbody>
      <tr>
        <td>alpha</td>
        <td>{{ alpha?.toFixed(2) }} deg</td>
      </tr>
      <tr>
        <td>beta</td>
        <td>{{ beta?.toFixed(2) }} deg</td>
      </tr>
      <tr>
        <td>gamma</td>
        <td>{{ gamma?.toFixed(2) }} deg</td>
      </tr>
      <tr>
        <td>absolute</td>
        <td>{{ absolute }}</td>
      </tr>
      <tr>
        <td>webkitCompassAccuracy</td>
        <td>{{ webkitCompassAccuracy }}</td>
      </tr>
      <tr>
        <td>webkitCompassHeading</td>
        <td>{{ webkitCompassHeading }}</td>
      </tr>
    </tbody>
  </table>
  <h1>Device Motion Event</h1>
  <table>
    <tbody>
      <tr>
        <td>rotationRateX</td>
        <td>{{ rotationRateX?.toFixed(2) }} deg/s</td>
      </tr>
      <tr>
        <td>rotationRateY</td>
        <td>{{ rotationRateY?.toFixed(2) }} deg/s</td>
      </tr>
      <tr>
        <td>rotationRateZ</td>
        <td>{{ rotationRateZ?.toFixed(2) }} deg/s</td>
      </tr>
      <tr>
        <td>accelerationX</td>
        <td>{{ accelerationX?.toFixed(2) }} m/s²</td>
      </tr>
      <tr>
        <td>accelerationY</td>
        <td>{{ accelerationY?.toFixed(2) }} m/s²</td>
      </tr>
      <tr>
        <td>accelerationZ</td>
        <td>{{ accelerationZ?.toFixed(2) }} m/s²</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  data() {
    return {
      navigator: navigator,
      screen: screen,
      window: window,
      connection: null,
      position: null,
      ipData: null,
      clipboard: '',
      x: 0,
      y: 0,
      z: 0,
      alpha: 0,
      beta: 0,
      gamma: 0,
      absolute: '',
      webkitCompassHeading: '',
      webkitCompassAccuracy: '',
      rotationRateX: 0,
      rotationRateY: 0,
      rotationRateZ: 0,
      accelerationX: 0,
      accelerationY: 0,
      accelerationZ: 0,
      drags: false
    }
  },
  watch: {
    alpha(newValue) {
      if (!newValue || !drags) return
      document.body.style.transformOrigin = `top center`;
      document.body.style.transform = `rotateZ(${newValue-90}deg)`
    }
  },
  methods: {
    getIpCity() {
      fetch('https://api.db-ip.com/v2/free/self')
        .then(res => res.json())
        .then(data => {
          this.ipData = data
        }).catch(err => console.log('Не удается получить айпи адрес: ', err))
    },
    accelerometr() {
      const acl = new Accelerometer({ frequency: 60 });
      acl.addEventListener("reading", () => {
        this.x = acl.x
        this.y = acl.y
        this.z = acl.z
      });
      acl.start();
    },
    deviceOrientation() {
      this.window.addEventListener('deviceorientation', (e) => {
        this.alpha = e.alpha
        this.beta = e.beta
        this.gamma = e.gamma
        this.absolute = e.absolute
        this.webkitCompassAccuracy = e.webkitCompassAccuracy
        this.webkitCompassHeading = e.webkitCompassHeading
      });
    },
    deviceMotion() {
      this.window.addEventListener('devicemotion', (e) => {
        this.rotationRateX = e.rotationRate.beta
        this.rotationRateY = e.rotationRate.gamma
        this.rotationRateZ = e.rotationRate.alpha
        this.accelerationX = e.acceleration.x
        this.accelerationY = e.acceleration.y
        this.accelerationZ = e.acceleration.z
      });
    },
    getBattery() {
      navigator.getBattery().then(battery => {
        this.batteryLevel = battery.level * 100;
        this.batteryCharging = battery.charging;
        this.batteryTimeRemaining = battery.dischargingTime;
        battery.addEventListener('levelchange', () => {
          this.batteryLevel = battery.level * 100;
        });
        battery.addEventListener('chargingchange', () => {
          this.batteryCharging = battery.charging;
        });
        battery.addEventListener('dischargingtimechange', () => {
          this.batteryTimeRemaining = battery.dischargingTime;
        });
      });
    }
  },
  created() {
    // navigator.clipboard.readText().then(clipText => {
    //   this.clipboard = clipText
    // });
    if ('connection' in navigator) {
      this.connection = navigator.connection;
    }
  },
  mounted() {
    navigator.geolocation.getCurrentPosition(position => {
      this.position = position;
    });
    this.getIpCity()
    this.accelerometr()
    this.deviceOrientation()
    this.deviceMotion()
    this.getBattery()
  }
}
</script>

<style>
table {
  width: 100%;
  border-collapse: collapse;
  border-spacing: 0
}

table,
td,
th {
  border: 1px solid #333333;
}

td,
th {
  padding: 10px 20px;
}

td:first-child {
  width: 40%;
}

td:last-child {
  color: #c0c0c0;
  width: 60%;
}
</style>
