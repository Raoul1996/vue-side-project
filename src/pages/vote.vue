<template lang="pug">
  .vote
    vote-list(:list="list")
</template>

<script>
  import voteList from '../components/voteList'
  import { mapState, mapActions } from 'vuex'

  export default {
    name: 'vote',
    data () {
      return {
        type: this.$route.path.slice(1)
      }
    },
    computed: {
      ...mapState(['list'])
    },
    created () {
      this.getVote()
    },
    methods: {
      ...mapActions(['getVoteListAction']),
      getVote () {
        const query = {
          page: 1,
          size: 100,
          time: 1,
          type: this.type
        }
        this.getVoteListAction(query)
      }
    },
    components: {
      voteList
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus" rel="stylesheet/stylus">
  // 三列布局

  .vote-list {
    margin 0 auto
    max-width: 1035px
    width 100%
    display flex
    flex-wrap wrap
    .vote-item {
      display inline-block
      margin 20px
      width 300px
    }
  }

  @media screen and (max-width: 690px) {
    .vote-list {
      .vote-item {
        margin 20px auto
      }
    }

  }
</style>
