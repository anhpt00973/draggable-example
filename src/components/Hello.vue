<template>
  <div class="fluid container">
    <div class="form-group form-group-lg panel panel-default">
      <div class="panel-heading">
        <h3 class="panel-title">Bảng sắp xếp</h3>
      </div>
      <div class="panel-body">
        <div class="checkbox">
          <label><input type="checkbox" v-model="editable">Kích hoạt tính năng kéo thả</label>
        </div>
        <button type="button" class="btn btn-default" @click="orderList">Sắp xếp theo thứ tự ban đầu</button>
      </div>
    </div>

    <div class="col-md-3">
      <draggable class="list-group" tag="ul" v-model="listData" v-bind="dragOptions" :move="onMove" @start="isDragging=true" @end="isDragging=false">
        <transition-group type="transition" :name="'flip-list'">
          <!-- <li class="list-group-item" v-for="element in list" :key="element.order">
            <i :class="element.fixed? 'fa fa-anchor' : 'glyphicon glyphicon-pushpin'" @click=" element.fixed=! element.fixed" aria-hidden="true"></i>
            {{element.name}}
            <span class="badge">{{element.order}}</span>
          </li> -->
          <li class="list-group-item" v-for="item in listData" :key="item.index"
            style="display: inline-flex;
            position: relative;
            cursor: move;
            resize: both;overflow: auto;">
              <i :class="item.fixed? 'fa fa-anchor' : 'glyphicon glyphicon-pushpin'" @click=" item.fixed=! item.fixed" aria-hidden="true" style="position:relative;
              "></i>
                <chart  :divId="item.index" :valueX="item.value" :nameX="item.name"
                height="200px" width="200px" 
                  style="display:grid;
                  
                  margin-right: -50px;
                  margin-bottom: -50px;
                  cursor: move;
                  "
                />
              <!-- <span class="badge">{{item.index}}</span> -->
          </li>
        </transition-group>
      </draggable>
    </div>

    <div class="col-md-3">
      <draggable element="span" v-model="list2" v-bind="dragOptions" :move="onMove">
        <transition-group name="no" class="list-group" tag="ul">
          <li class="list-group-item" v-for="item in list2" :key="item.index">
            <i :class="item.fixed? 'fa fa-anchor' : 'glyphicon glyphicon-pushpin'" @click=" item.fixed=! element.fixed" aria-hidden="true"></i>
            {{item.name}}
            <span class="badge">{{item.id}}</span>
          </li>

        </transition-group>
      </draggable>
    </div>

    <div class="list-group col-md-3">
      <pre>{{listString}}</pre>
    </div>
    <div class="list-group col-md-3">
      <pre>{{list2String}}</pre>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import Chart from '@/components/RadialChart'



export default {
  name: "hello",
  components: {
    draggable, Chart
  },
  data() {
    return {
      list2: [],
      editable: true,
      isDragging: false,
      delayedDragging: false,
      listData: [
				{ index: '0', value: '10', name: 'core1', fixed: false },
				{ index: '1', value: '20', name: 'core2', fixed: false },
				{ index: '2', value: '30', name: 'core3', fixed: false },
				{ index: '3', value: '40', name: 'core4', fixed: false },
				{ index: '4', value: '50', name: 'core5', fixed: false },
				{ index: '5', value: '60', name: 'core6', fixed: false }
			]
    };
  },
  methods: {
    orderList() {
      this.listData = this.listData.sort((one, two) => {
        return one.index - two.index;
      });
    },
    onMove({ relatedContext, draggedContext }) {
      const relatedElement = relatedContext.element;
      const draggedElement = draggedContext.element;
      return (
        (!relatedElement || !relatedElement.fixed) && !draggedElement.fixed
      );
    }
  },
  computed: {
    dragOptions() {
      return {
        animation: 0,
        group: "description",
        disabled: !this.editable,
        ghostClass: "ghost"
      };
    },
    listString() {
      return JSON.stringify(this.listData, null, 2);
    },
    list2String() {
      return JSON.stringify(this.list2, null, 2);
    }
  },
  watch: {
    isDragging(newValue) {
      if (newValue) {
        this.delayedDragging = true;
        return;
      }
      this.$nextTick(() => {
        this.delayedDragging = false;
      });
    }
  }
};
</script>

<style>
.flip-list-move {
  transition: transform 0.5s;
}

.no-move {
  transition: transform 0s;
}

.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}

.list-group {
  min-height: 20px;
}

.list-group-item {
  cursor: move;
}

.list-group-item i {
  cursor: pointer;
}
</style>
