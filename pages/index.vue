<template>
  <section class="section">
    <div class="columns is-centered is-vcentered">
      <div class="column is-narrow">
        <b-field label="Date of Birth" label-position="inside">
          <b-datepicker
            type="month"
            v-model="dob"
            placeholder="Click to select..."
            icon="calendar-today"
            :mobile-native="false"
            trap-focus
          >
          </b-datepicker>
        </b-field>
      </div>
      <div class="column is-narrow">
        <b-field label="Joined Date" label-position="inside">
          <b-datepicker
            type="month"
            v-model="joinedDate"
            placeholder="Click to select..."
            icon="calendar-today"
            :mobile-native="false"
            trap-focus
          >
          </b-datepicker>
        </b-field>
      </div>
      <div class="column is-narrow">
        <b-message type="is-success" size="is-small">
          <strong>Formula:</strong> Base Formula x Quantifier x Last Salary
        </b-message>
      </div>
    </div>
    <nav class="level section">
      <div class="level-item has-text-centered">
        <div>
          <p class="heading">Age</p>
          <p class="title">{{ age }}</p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="heading">Base Formula</p>
          <p class="title">{{ baseFormula }}</p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="heading">Approach</p>
          <p class="title has-text-info">{{ approach }}</p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="heading">Year of Service</p>
          <p class="title">{{ yearOfService }}</p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="heading">Months Until Retire</p>
          <p class="title">{{ monthsUntilRetire }}</p>
        </div>
      </div>
    </nav>
    <section class="hero is-primary">
      <div class="hero-body">
        <p class="title">Result</p>
        <p class="subtitle">
          {{ baseFormula }} x {{ quantifier }} = {{ quantom }} months
        </p>
      </div>
    </section>
    <div class="columns my-5">
      <div class="column">
        <b-field label="Your Salary (Optional)">
          <b-numberinput v-model="salary" :controls="false"> </b-numberinput>
        </b-field>
      </div>
      <div class="column">
        <b-field label="Amount (MYR)">
          <b-numberinput
            v-model="amount"
            :editable="false"
            :controls="false"
          ></b-numberinput>
        </b-field>
      </div>
    </div>

    <b-collapse class="card my-5" animation="slide" :open="false">
      <template #trigger="props">
        <div
          class="card-header"
          role="button"
          aria-controls="contentIdForA11y3"
        >
          <p class="card-header-title">Debugging</p>
          <a class="card-header-icon">
            <b-icon :icon="props.open ? 'menu-down' : 'menu-up'"> </b-icon>
          </a>
        </div>
      </template>

      <div class="card-content">
        <div class="content">
          <pre>
          {{ dob.toISOString() }}
          {{ joinedDate.toISOString() }}
          {{ retiringAge.toISOString() }}
         </pre
          >
        </div>
      </div>
    </b-collapse>

    <div class="section"></div>
  </section>
</template>

<script>
export default {
  name: "HomePage",

  data() {
    return {
      salary: 0,
      dob: this.$dayjs("02/04/1985").toDate(),
      joinedDate: this.$dayjs("01/01/2009").toDate(),
      eighteenYearsOld: this.$dayjs().subtract(18, "year").toDate(),
      retired: this.$dayjs().subtract(60, "year").toDate(),
      lastMonth: this.$dayjs().subtract(1, "month").toDate(),
    };
  },
  filters: {
    format(value) {
      return value.toLocaleString();
    },
  },
  methods: {
    hoorey() {
      this.$confetti.start();
      setTimeout(() => this.$confetti.stop(), 1500);
    },
  },
  watch: {
    // when input reached minimum salary
    salary: function (newSalary, oldSalary) {
      if (newSalary > 3500) this.hoorey();
    },
  },
  computed: {
    age() {
      return this.$dayjs().diff(this.dob, "year");
    },
    baseFormula() {
      return this.age >= 55 ? 0.5 : 1.5;
    },
    approach() {
      return this.age >= 55 ? "Months until Retire" : "Years of Service";
    },
    quantifier() {
      let base = this.age >= 55 ? this.monthsUntilRetire : this.yearOfService;

      return base <= 36 ? base : 36;
    },
    yearOfService() {
      return this.$dayjs().diff(this.joinedDate, "years");
    },
    retiringAge() {
      return this.$dayjs(this.dob).add(60, "years");
    },
    monthsUntilRetire() {
      return Math.abs(this.$dayjs().diff(this.retiringAge, "months"));
    },
    quantom() {
      return this.baseFormula * this.quantifier;
    },
    amount() {
      return this.baseFormula * this.quantifier * this.salary;
    },
  },
};
</script>
