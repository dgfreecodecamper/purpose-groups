<template>
	<v-app>
		<!-- header -->
		<v-toolbar dark color="primary">
			<v-toolbar-title>Purpose Groups</v-toolbar-title>
		</v-toolbar>

		<v-content>
			<v-container fluid>
				<!-- first row of content to hold the form -->
				<v-layout row>
					<v-flex>
						<!-- <v-form ref="form" v-model="valid" lazy-validation> -->
						<v-form ref="form" v-on:submit.prevent>

							<v-select :items="buildTypeOpts" v-model="buildType" label="Flat or Dwelling" max-height="800" outline v-on:change="calculate"></v-select>

							<v-select :items="workTypeOpts" v-model="workType" label="Type of work" maxHeight="800" outline v-on:change="calculate"></v-select>

							<v-select :items="devTypeOpts" v-model="devType" label="Development Type" maxHeight="800" outline v-on:change="calculate"></v-select>

							<v-select :items="subType1Opts" v-model="subType1" label="Sub Group" maxHeight="800" outline v-on:change="calculate"></v-select>

							<v-select :items="subType2Opts" v-model="subType2" label="Other grouping" maxHeight="800" outline v-on:change="calculate"></v-select>

							<v-switch :label="`Multiple Works: ${multi.toString()}`" v-model="multi" v-on:change="calculate"></v-switch>

							<h1 class="font-weight-thin text-xs-center">Purpose Group</h1>
							<h2 class="font-weight-bold text-xs-center display-3">{{result}}</h2>

						</v-form>
					</v-flex>
				</v-layout>
			</v-container>
		</v-content>

		<v-footer height="auto" color="primary lighten-1">
			<v-layout justify-center row wrap>
				<v-btn v-for="link in links" :key="link" color="white" flat round>
					{{ link }}
				</v-btn>
				<v-flex primary lighten-2 py-3 text-xs-center white--text xs12>
					&copy;2018 —
					<strong>Built with Vuetify</strong>
				</v-flex>
			</v-layout>
		</v-footer>
	</v-app>
</template>

<script>
export default {
	name: 'MainPage',
	props: {
		// msg: String
	},
	data: () => {
		return {
			buildTypeOpts: [
				{ text: 'Flat / Maisonette (1a)', value: '1A' },
				{ text: 'Dwelling floor > 4.5m (3 Storey) (1b)', value: '1B' },
				{ text: 'Dwelling floor < 4.5m (2 Storey) (1c)', value: '1C' },
				{ text: 'Domestic Garage (1g)', value: '1G' },
				{ text: 'Residential (Institutional) - Hospital (2a)', value: '2A' },
				{
					text: 'Residential (Institutional) - HMO / College (2b)',
					value: '2B'
				},
				{
					text: 'Residential (Institutional) - Hotel / Hostel (2c)',
					value: '2C'
				},
				{ text: 'Office (3)', value: '3' },
				{ text: 'Shop / Commercial (4)', value: '4' },
				{ text: 'Assembly and Recreation (5)', value: '5' },
				{ text: 'Industrial (6)', value: '6' },
				{ text: 'Storage (7a)', value: '7A' },
				{ text: 'Car Parks (7b)', value: '7B' }
			],
			buildType: '',

			workTypeOpts: [
				{ text: 'New Build - Greenfield (NG)', value: 'NG' },
				{ text: 'New Build - Brownfield (NB)', value: 'NB' },
				{ text: 'Extension and/or Alterations (X)', value: 'X' },
				{ text: 'Services and/or Fittings (S)', value: 'S' },
				{ text: 'Change of Use (U)', value: 'U' }
			],
			workType: '',

			devTypeOpts: [
				{ text: 'Private owner occupied (P)', value: 'P' },
				{ text: 'Speculative development (S)', value: 'S' },
				{ text: 'Housing Executive (H)', value: 'H' },
				{ text: 'Housing Association (A)', value: 'A' }
			],
			devType: '',

			subType1Opts: [
				{ text: 'Detached (D)', value: 'D' },
				{ text: 'Semi-detached (S)', value: 'S' },
				{ text: 'Terraced (T)', value: 'T' },
				{ text: 'Part of larger building (P)', value: 'P' },
				{ text: 'Extension (E)', value: 'E' },
				{ text: 'Alterations / improvements (A)', value: 'A' },
				{ text: 'Roofspace (RS)', value: 'RS' },
				{ text: 'Attached / Integral garage (AG)', value: 'AG' },
				{ text: 'Central Heating (CH)', value: 'CH' },
				{ text: 'Sanitary Fittings (SF)', value: 'SF' }
			],
			subType1: '',

			subType2Opts: [
				{ text: 'Single Storey (1)', value: '1' },
				{ text: 'Two Storey (2)', value: '2' },
				{ text: 'More than 2 storey (3)', value: '3' },
				{ text: 'Storage (S)', value: 'S' },
				{ text: 'Habitable (H)', value: 'H' },
				{ text: 'Installation (A)', value: 'A' },
				{ text: 'Conversion (C)', value: 'C' },
				{ text: 'Other (O)', value: 'O' }
			],
			subType2: '',

			multi: false,
			result: '-----------',
			links: ['home']
		};
	},
	methods: {
		calculate: function() {
			this.result =
				`${this.buildType}${this.workType}${this.devType}${this.subType1}${
					this.subType2
				}${this.multi ? 'M' : ''}` || '----------';
		}
	},
	watch: {
		buildType: function() {
			this.workType = this.devType = this.subType1 = this.subType2 = '';
			this.multi = false;
			this.calculate();
		},
		workType: function() {
			this.devType = this.subType1 = this.subType2 = '';
			this.multi = false;
			this.calculate();
		},
		devType: function() {
			this.subType1 = this.subType2 = '';
			this.multi = false;
			this.calculate();
		},
		subType1: function() {
			this.subType2 = '';
			this.multi = false;
			this.calculate();
		},
		subType2: function() {
			this.multi = false;
			this.calculate();
		},
		multi: function() {
			this.calculate();
		}
	}
};
</script>
