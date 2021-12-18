<template>
  <div :class="gridView ? 'd-flex' : ''">
    <q-table
      title="Treats"
      :class="gridView ? 'width30' : ''"
      :rows="rows"
      :columns="columns"
      row-key="fat"
      :selected-rows-label="getSelectedString"
      selection="multiple"
      v-model:selected="selected"
      hide-header
      hide-bottom
      :grid="gridView"
    >
      <template v-slot:top class="q-mb-md">
        <q-checkbox v-model="val" color="cyan-8" />

        <div class="mailIcon" v-if="gridView">
          <q-chip
            flat
            square
            color="transparent"
            text-color="grey-8"
            icon="forward"
          >
            Forward
          </q-chip>
          <q-chip
            flat
            square
            color="transparent"
            text-color="grey-8"
            icon="reply"
          >
            Reply
          </q-chip>
        </div>

        <q-icon name="more_horiz" color="grey-8" size="sm" class="q-mr-md" />
        <q-space />
        <div class="tableHead" v-if="!gridView">
          <span> Sorted By </span>
          <q-icon name="expand_more" color="cyan-8" size="sm" class="q-mr-md" />
          <q-icon
            name="view_sidebar"
            style="cursor: pointer"
            :color="!gridView ? 'grey-8' : 'amber-6'"
            size="sm"
            class="q-mr-md"
            @click="gridView = true"
          />
          <q-icon
            name="calendar_view_day"
            style="cursor: pointer"
            :color="gridView ? 'grey-8' : 'amber-6'"
            size="sm"
            class="q-mr-md"
            @click="gridView = false"
          />
        </div>
      </template>

      <template v-slot:body="props" v-if="!gridView">
        <q-tr :props="props">
          <q-td auto-width>
            <q-checkbox
              dense
              v-model="props.selected"
              color="amber-6"
              class="text-weight-medium"
            />
            <q-rating
              v-model="props.selected"
              size="2em"
              :max="1"
              color="grey-8"
              icon="star_border"
              icon-selected="star"
            />
          </q-td>
          <q-td auto-width>
            <q-badge
              rounded
              color="amber-6"
              v-if="props.cols[0].value == 'Marc John'"
            />
          </q-td>
          <q-td v-for="col in props.cols" :key="col.name" :props="props">
            {{ col.value }}
          </q-td>
          <q-td class="text-right">
            <img
              alt="Vue logo"
              v-if="
                props.row.fat == 'New Envelope' || props.row.fat == 'Receipt'
              "
              src="../assets/envelope.svg"
            />
          </q-td>
        </q-tr>
      </template>

      <template v-slot:item="props" v-if="gridView">
        <div
          class="
            q-pa-xs
            col-xs-12 col-sm-12 col-md-12 col-lg-12
            grid-style-transition
          "
        >
          <q-card
            :class="props.selected ? 'bg-grey-2' : ''"
            :style="
              props.selected
                ? ' background: #E4F5F5 !important; border-radius: 3px;'
                : ''
            "
          >
            <q-card-section style="padding-bottom: 0px !important">
              <div class="row items-baseline no-wrap">
                <div class="col" style="padding: 0px 5px">
                  <q-checkbox
                    dense
                    v-model="props.selected"
                    :label="props.row.calories"
                    color="amber-6"
                    class="text-weight-medium"
                  />
                </div>
                <div class="col-auto">
                  <p style="margin-bottom: 5px">{{ props.row.carbs }}</p>
                </div>
              </div>
            </q-card-section>
            <q-list dense>
              <q-item
                v-for="col in props.cols.filter(
                  (col) =>
                    col.name !== 'desc' &&
                    col.name !== 'calories' &&
                    col.name !== 'carbs'
                )"
                :key="col.name"
              >
                <q-item-section style="padding: 0px 45px" class="q-mb-md">
                  <q-item-label class="text-weight-medium">{{
                    props.row.fat
                  }}</q-item-label>
                </q-item-section>
              </q-item>
              <q-item-section style="padding: 0px 59px">
                <div class="row items-center no-wrap q-mb-md">
                  <div class="col" style="padding: 0px 5px">
                    <q-item-label
                      v-if="
                        props.row.fat == 'New Envelope' ||
                        props.row.fat == 'Receipt'
                      "
                      class="q-mb-md"
                      ><img alt="Vue logo" src="../assets/envelope.svg" />
                    </q-item-label>
                  </div>
                  <div class="col-auto text-right">
                    <q-rating
                      v-model="ratingModel"
                      size="2em"
                      :max="1"
                      color="grey-8"
                      icon="star_border"
                      icon-selected="star"
                    />
                  </div>
                </div>
              </q-item-section>
            </q-list>
          </q-card>
        </div>
      </template>
    </q-table>
    <div class="q-mt-lg" :class="gridView ? 'width70 ' : ''" v-if="gridView">
      <div class="cardHead q-mb-md text-right">
        <span> Sorted By </span>
        <q-icon name="expand_more" color="cyan-8" size="sm" class="q-mr-md" />
        <q-icon
          name="view_sidebar"
          style="cursor: pointer"
          :color="!gridView ? 'grey-8' : 'amber-6'"
          size="sm"
          class="q-mr-md"
          @click="gridView = true"
        />
        <q-icon
          name="calendar_view_day"
          style="cursor: pointer"
          :color="gridView ? 'grey-8' : 'amber-6'"
          size="sm"
          class="q-mr-md"
          @click="gridView = false"
        />
      </div>
      <q-card flat bordered class="my-card bg-grey-1">
        <q-card-section class="headerSec">
          <div class="row items-center no-wrap">
            <div class="col">
              <div class="text-h6 text-bold">New Employee</div>
            </div>
            <div class="col-auto">
              <q-icon
                name="print"
                style="cursor: pointer"
                color="grey-8"
                size="sm"
                class="q-mr-md"
              />
              <q-icon
                name="file_download"
                style="cursor: pointer"
                color="grey-8"
                size="sm"
                class="q-mr-md"
              />
              <q-icon
                name="close"
                style="cursor: pointer"
                color="grey-8"
                size="sm"
                class="q-mr-md"
              />
            </div>
          </div>
        </q-card-section>

        <q-card-section>
          <div class="row items-baseline no-wrap">
            <div class="col" style="padding: 0px 20px">
              <p style="margin-bottom: 10px">marc.john@email.com</p>
              <p>23-1-2021 19:05AM</p>
            </div>
            <div class="col-auto">
              <q-icon
                name="forward"
                style="cursor: pointer"
                color="grey-8"
                size="sm"
                class="q-mr-md"
              />

              <q-icon
                name="reply"
                style="cursor: pointer"
                color="grey-8"
                size="sm"
                class="q-mr-md"
              />
              <q-icon
                name="more_horiz"
                color="grey-8"
                size="sm"
                class="q-mr-md"
              />
            </div>
          </div>
        </q-card-section>

        <q-card-actions class="justify-center w-100">
          <img alt="Vue logo" src="../assets/email.svg" style="width: 90%" />
        </q-card-actions>
      </q-card>
    </div>
  </div>
</template>
<script>
import { ref } from "vue";

const columns = [
  {
    name: "calories",
    align: "left",
    label: "Calories",
    field: "calories",
    sortable: true,
  },

  {
    name: "fat",
    label: "Fat (g)",
    field: "fat",
    sortable: true,
    align: "left",
  },
  { name: "carbs", label: "Carbs (g)", field: "carbs", align: "center" },
];

const rows = [
  {
    calories: "Marc John",
    fat: "New Envelope",
    carbs: "23-1-2021",
  },
  {
    calories: "Marc John",
    fat: "New Updates",
    carbs: "23-1-2021",
  },
  {
    calories: "Bank",
    fat: "Receipt",
    carbs: "22-1-2021",
  },
  {
    calories: "Emy Wilson",
    fat: "Upcoming webinar",
    carbs: "21-1-2021",
  },
  {
    calories: "David Walker",
    fat: "Resurces to help reach your...",
    carbs: "21-1-2021",
  },
  {
    calories: "Asana",
    fat: "Daily work summry",
    carbs: "23-1-2021",
  },
];

export default {
  setup() {
    const selected = ref([]);

    return {
      selected,
      columns,
      rows,
      ratingModel: ref(),
      val: ref(true),
      gridView: ref(false),
      getSelectedString() {
        return selected.value.length === 0
          ? ""
          : `${selected.value.length} record${
              selected.value.length > 1 ? "s" : ""
            } selected of ${rows.length}`;
      },
    };
  },
};
</script>

<style >
.q-table--grid .q-table__grid-content {
  flex-direction: column !important;
}
.q-table__grid-item {
  width: 100% !important;
}
.headerSec {
  background: #e4f5f5;
  border-radius: 3px;
}
.q-checkbox--dense .q-checkbox__inner {
  margin-right: 15px !important;
}
.q-table__container > div:first-child {
  padding-left: 15px !important;
}
.d-flex {
  display: flex;
}
.width30 {
  width: 30%;
}
.width70 {
  width: 70%;
}
@media only screen and (max-width: 1306px) {
  .d-flex {
    flex-direction: column-reverse;
  }
  .width30,
  .width70 {
    width: 100%;
  }
}
</style>