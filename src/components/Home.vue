<template lang="pug">
  .content-wrapper
    section
      .container
        h1.ui-title-1 Home
        input(
        type="text"
          placeholder="Что будем смотреть?"
          v-model="taskTitle"
          @keyup.enter="newTask"
        )
        textarea(
          type="text"
          v-model="taskDescription"
          @keyup.enter="newTask"
        )
        .option-list
          input.what-watch--radio(
            type="radio"
            id="radioFilm"
            value="Film"
            v-model="whatWatch"
          )
          label(
            for="radioFilm"
          ) Фильм
          input.what-watch--radio(
            type="radio"
            id="radioSerial"
            value="Serial"
            v-model="whatWatch"
          )
          label(
            for="radioSerial"
          ) Сериал
        .total-time
          .total-time__film(
            v-if="whatWatch === 'Film'"
          )
            span Total Film Times
          .total-time__serial(
          v-if="whatWatch === 'Serial'"
          )
            span Total Serial Times
        .tag-list
          .ui-tag__wrapper
            .ui-tag
              span.tag-title DOGS
              span.button-close
    section
      .container
        .task-list
          .task-item(
          v-for="task in tasks"
          :key="task.id"
          :class="{ completed: task.completed }"
          )
            .ui-card.ui-card--shadow
              .task-item__info
                .task-item__main-info
                  span.ui-label.ui-label--light {{ task.whatWatch }}
                  span Total Time:
                span.button-close
              .task-item__content
                .task-item__header
                  .ui-checkbox-wrapper
                    input.ui-checkbox(
                    type='checkbox'
                    v-model="task.completed"
                    )
                  span.ui-title-3 {{ task.title }}
                .task-item__body
                  p.ui-text-regular {{ task.description }}
</template>

<script>
export default {
  data () {
    return {
      taskTitle: '',
      taskDescription: '',
      whatWatch: 'Film',
      taskId: 3,
      tasks: [
        {
          'id': 1,
          'title': 'Начало',
          'description': 'Крутейший фильм с Леонардо Дикаприо',
          'whatWatch': 'Film',
          'completed': false,
          'editing': false
        },
        {
          'id': 2,
          'title': 'Клан Сопрано',
          'description': 'Один из интереснейших сериалов про итальянскую мафию',
          'whatWatch': 'Serial',
          'completed': false,
          'editing': false
        }
      ]
    }
  },
  methods: {
    newTask () {
      if (this.taskTitle === '' || this.taskDescription === '') {
        return
      }
      this.tasks.push({
        id: this.taskId,
        title: this.taskTitle,
        description: this.taskDescription,
        whatWatch: this.whatWatch,
        completed: false,
        edited: false
      })

      // Reset
      this.taskId += 1
      this.taskTitle = ''
      this.taskDescription = ''
    }
  }
}
</script>

<style lang="stylus" scoped>
  .option-list
    display flex
    .what-watch--radio
      margin-right 12px
    label
      margin-right 20px
      &:last-child
        margin-right 0

  .task-item
    margin-bottom 20px

  .ui-label
    margin-right 8px

    &:last-child
      margin-bottom 0

  .task-item__info
    display flex
    align-item center
    justify-content space-between
    margin-bottom 20px

    .button-close
      width 20px
      height @width

  .task-item__header
    display flex
    align-items center
    margin-bottom 20px

    .ui-checkbox-wrapper
      margin-right 8px

  /*.ui-title-3*/
    /*margin-bottom 0*/
</style>
