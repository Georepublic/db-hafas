# db-hafas

**A client for the German Railways (DB).** It acts as a consistent and straightforward interface on top of a verbose API.

This project is actually a thin wrapper around [`hafas-client@6`](https://github.com/public-transport/hafas-client/blob/6/readme.md). [Its docs](https://github.com/public-transport/hafas-client/blob/6/docs/readme.md) document the API in general.

![db-rest architecture diagram](https://rawgit.com/derhuerst/db-rest/master/architecture.svg)

[![npm version](https://img.shields.io/npm/v/db-hafas.svg)](https://www.npmjs.com/package/db-hafas)
![ISC-licensed](https://img.shields.io/github/license/public-transport/db-hafas.svg)
[![support me via GitHub Sponsors](https://img.shields.io/badge/support%20me-donate-fa7664.svg)](https://github.com/sponsors/derhuerst)
[![chat with me on Twitter](https://img.shields.io/badge/chat%20with%20me-on%20Twitter-1da1f2.svg)](https://twitter.com/derhuerst)


## Installing

```shell
npm install db-hafas
```


## API

Check [the docs for `hafas-client@6`](https://github.com/public-transport/hafas-client/tree/6/docs) as well as [its DB-specific customisations](https://github.com/public-transport/hafas-client/blob/6/p/db/readme.md).


## Getting Started

```javascript
import {createDbHafas} from 'db-hafas'

const hafas = createDbHafas('my-awesome-program')
```

As an example, we will search for a route from *Berlin Jungfernheide* to *München Hbf*. To get the station IDs, use [`locations(query, [opt])`](https://github.com/public-transport/hafas-client/blob/6/docs/locations.md).

```javascript
// Berlin Jungfernheide to München Hbf
const journeys = await hafas.journeys('8011167', '8000261', {
	results: 1,
})
console.log(journeys[0])
```

The output will be an array of [`journey` objects in the *Friendly Public Transport Format* `1.2.1` format](https://github.com/public-transport/friendly-public-transport-format/tree/1.2.1/spec#journey):

```javascript
[ {
	type: 'journey',
	legs: [ {
		tripId: '1|300793|27|80|27032019',
		origin: {
			type: 'stop',
			id: '8089100',
			name: 'Berlin Jungfernheide (S)',
			location: {
				type: 'location',
				id: '8089100',
				latitude: 52.530408,
				longitude: 13.299424
			},
			products: {
				nationalExpress: false,
				national: false,
				regionalExp: false,
				regional: true,
				suburban: true,
				bus: true,
				ferry: false,
				subway: true,
				tram: false,
				taxi: false
			},
			station: {
				type: 'station',
				id: '8011167',
				name: 'Berlin Jungfernheide',
				location: { /* … */ },
				products: { /* … */ }
			}
		},
		departure: '2019-03-27T14:10:00.000+01:00',
		departureDelay: 0,
		departurePlatform: '6',
		destination: {
			type: 'stop',
			id: '8089073',
			name: 'Berlin Südkreuz (S)',
			location: { /* … */ },
			products: { /* … */ },
			station: { /* … */ }
		},
		arrival: '2019-03-27T14:30:00.000+01:00',
		arrivalDelay: 0,
		arrivalPlatform: '12',
		direction: 'Berlin Südkreuz (S)',
		line: {
			type: 'line',
			id: 's-42',
			fahrtNr: '42133',
			name: 'S 42',
			public: true,
			mode: 'train',
			product: 'suburban',
			operator: {type: 'operator', id: 's-bahn-berlin', name: 'S-Bahn Berlin'}
		},
		cycle: {min: 300, max: 300, nr: 25}
	}, {
		origin: { /* … */ },
		departure: '2019-03-27T14:30:00.000+01:00',
		destination: { /* … */ },
		arrival: '2019-03-27T14:37:00.000+01:00',
		public: true,
		walking: true,
		distance: 622
	}, {
		tripId: '1|245684|0|80|27032019',
		origin: { /* … */ },
		departure: '2019-03-27T14:37:00.000+01:00',
		departureDelay: 0,
		departurePlatform: '3',
		destination: {
			type: 'stop',
			id: '8000261',
			name: 'München Hbf',
			location: { /* … */ },
			products: { /* … */ }
		},
		arrival: '2019-03-27T19:06:00.000+01:00',
		arrivalDelay: 0,
		arrivalPlatform: '18',
		direction: 'München Hbf'
		line: {
			type: 'line',
			id: 'ice-1601',
			fahrtNr: '1601',
			name: 'ICE 1601',
			public: true,
			mode: 'train',
			product: 'nationalExpress',
			operator: { /* … */ }
		},
	} ],
	refreshToken: '…',
	price: {amount: null, hint: 'No pricing information available.'}
} ]
```


## Similar Projects

- [Fahrplan.js](https://github.com/pbock/fahrplan) – "A JavaScript client for Deutsche Bahn's timetable API"
- [db-prices](https://github.com/juliuste/db-prices) – Find the cheapest routes using the DB Sparpreise API.
- [db-stations](https://github.com/derhuerst/db-stations) – An offline list of all DB stations.

Also check [`hafas-client`'s related projects](https://github.com/public-transport/hafas-client/blob/6/readme.md#related-projects).


## Contributing

If you **have a question**, **found a bug** or want to **propose a feature**, have a look at [the issues page](https://github.com/public-transport/db-hafas/issues).
