<template>
  <h1>Устройство</h1>
  <table>
    <tbody>
      <tr>
        <td>Платформа:</td>
        <td>{{ navigator.userAgentData.platform }}</td>
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
      <tr>
        <td>Содержимое буфера обмена:</td>
        <td>{{ clipboard }}</td>
      </tr>
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
        <td>Сайт из которого сюда пришел</td>
        <td>{{ document?.referrer }}</td>
      </tr>
      <tr>
        <td>Количество страниц в истории данной вкладки</td>
        <td>{{ window.history.length }}</td>
      </tr>
      <tr>
        <td>Устройство мобильное</td>
        <td>{{ navigator.userAgentData.mobile }}</td>
      </tr>
      <tr>
        <td>Brands</td>
        <td>
          <p v-for="item in navigator.userAgentData.brands">{{ item.brand }}, version: {{ item.version }}</p>
        </td>
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
  <h1 v-if="accelerometer">Акселерометр</h1>
  <table v-if="accelerometer">
    <tbody>
      <tr>
        <td>Координата x</td>
        <td>{{ x.toFixed(2) }}</td>
      </tr>
      <tr>
        <td>Координата y</td>
        <td>{{ y.toFixed(2) }}</td>
      </tr>
      <tr>
        <td>Координата z</td>
        <td>{{ z.toFixed(2) }}</td>
      </tr>
    </tbody>
  </table>
  <h1>Датчик света</h1>
  <table>
    <tbody>
      <tr>
        <td>devicelight</td>
        <td>{{ devicelight }}</td>
      </tr>
      <tr>
        <td>deviceproximity</td>
        <td>{{ deviceproximity }}</td>
      </tr>
      <tr>
        <td>userproximity</td>
        <td>{{ userproximity }}</td>
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
      deviceproximity: '',
      devicelight: '',
      userproximity: '',
      accelerometer: true,
      x: 0,
      y: 0,
      z: 0,
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
    strangeThings() {
      if (typeof window.ondeviceproximity === "undefined") {
        this.deviceproximity = "This browser does not support the ondeviceproximity event"
      } else {
        window.ondeviceproximity = function (event) {
          this.deviceproximity = event.value
        }
      }
      if (typeof window.ondevicelight === "undefined") {
        this.devicelight = "This browser does not support the ondevicelight event"
      } else {
        window.ondevicelight = function (event) {
          this.devicelight = event.value
        }
      }
      if (typeof window.onuserproximity === "undefined") {
        this.userproximity = "This browser does not support the onuserproximity event"
      } else {
        window.onuserproximity = function (event) {
          this.userproximity = event.value
        }
      }
      if ('Accelerometer' in this.window) {
        const acl = new Accelerometer({ frequency: 60 });
        acl.addEventListener("reading", () => {
          this.x = acl.x
          this.y = acl.y
          this.z = acl.z
        });
        acl.start();
      } else {
        this.accelerometer = false
      }
    }
  },
  created() {
    navigator.clipboard.readText().then(clipText => {
      this.clipboard = clipText
    });
    if ('getBattery' in navigator) {
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
    if ('connection' in navigator) {
      this.connection = navigator.connection;
    }
  },
  mounted() {
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(position => {
        this.position = position;
      });
    } else {
      console.log("Geolocation is not supported by this browser.");
    }
    this.getIpCity()
    this.strangeThings()
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
