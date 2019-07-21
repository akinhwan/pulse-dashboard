<template>
  <div class="row">
    <div class="col-md-8">
      <edit-profile-form :model="model">
      </edit-profile-form>
    </div>
    <div class="col-md-4">
      <user-card :user="user"></user-card>
    </div>
  </div>
</template>
<script>
  import EditProfileForm from './Profile/EditProfileForm';
  import UserCard from './Profile/UserCard'
  export default {
    components: {
      EditProfileForm,
      UserCard
    },
    data() {
      return {
        model: {
          company: 'Creative Code Inc.',
          email: 'mike@email.com',
          username: 'michael23',
          firstName: 'Mike',
          lastName: 'Andrew',
          address: 'Bld Mihail Kogalniceanu, nr. 8 Bl 1, Sc 1, Ap 09',
          city: 'Melbourne',
          country: 'Australia',
          about: 'The patient satisfaction dashboard is the showcase of your healthcare facility. It will translate the efforts you put in welcoming and treating your patients, as well as the degree of safety you deliver to them. Unsatisfied patients will neither return in case of a problem, nor recommend your facility to friends and family. At the internet age, the viral spread of “bad buzz” can be harmful and hard to contain. The use of this type of healthcare dashboard can be an asset, especially in the communication with your patients. Healthcare is a very specific industry because it is exposed to a lot of human subjectivity and it deals with high stakes, the health and life of people. Communication and understanding is often cited as an important aspect in the doctor-patient relationship, this is why such dashboard can benefit your services a lot. Patients like good quality of care, which requires their feedback.'
        },
        user: {
          fullName: 'Mike Andrew',
          title: 'Ceo/Co-Founder',
          description: `Do not be scared of the truth because we need to restart the human foundation in truth And I love you like Kanye loves Kanye I love Rick Owens’ bed design but the back is...`,
        }
      }
    }
  }
</script>
<style>
</style>
