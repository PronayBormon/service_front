<template>
  <div>

    <div class="col-lg-12" style="margin-top: 10px;;">
      <div class="ui-content container">
        <div class="navpill-style1">
          <ul class="nav overflow_auto nav-pills mb12" id="pills-tab" role="tablist">
            <li class="nav-item" role="presentation">
              <button class="nav-link active fw500 dark-color" id="pills-home-tab" data-bs-toggle="pill"
                data-bs-target="#pills-home" type="button" role="tab" aria-controls="pills-home" aria-selected="true"><i
                  class="fa fa-grid" aria-hidden="true"></i>&nbsp;Dashboard</button>
            </li>

            <li class="nav-item" role="presentation">
              <button class="nav-link fw500 dark-color" @click="chatbox"><i class="fa fa-commenting"
                  aria-hidden="true"></i>&nbsp;Messages</button>
            </li>
            <li class="nav-item" role="presentation">
              <button class="nav-link fw500 dark-color" @click="myprofile" aria-selected="false"><i class="fa fa-user"
                  aria-hidden="true"></i>&nbsp;Profile</button>
            </li>

            <li class="nav-item" role="presentation">
              <button class="nav-link fw500 dark-color" @click="deposit" aria-selected="false"><i
                  class="far fa-money-bill-alt" aria-hidden="true"></i>&nbsp;Deposit</button>
            </li>
            <li class="nav-item" role="presentation">
              <button class="nav-link fw500 dark-color" @click="mywithdraw" aria-selected="false">
                <i class="	fas fa-dollar-sign" aria-hidden="true"></i>&nbsp;Withdraw </button>
            </li>

            <li class="nav-item" role="presentation">
              <button class="nav-link fw500 dark-color" @click="myorders" aria-selected="false"><i
                  class="fa fa-shopping-cart" aria-hidden="true"></i>&nbsp;Orders</button>
            </li>

            <li class="nav-item" role="presentation">
              <button class="nav-link fw500 dark-color" @click="mlm" aria-selected="false"><i class="fa fa-user"
                  aria-hidden="true"></i>&nbsp;Community</button>
            </li>

            <li class="nav-item" role="presentation">
              <button class="nav-link fw500 dark-color" @click="mysetting" aria-selected="false"><i class="fa fa-cogs"
                  aria-hidden="true"></i>&nbsp;Setting</button>
            </li>
            <li class="nav-item d-none" role="presentation">
              <button class="nav-link fw500 dark-color" id="#" data-bs-toggle="pill" data-bs-target="#" type="button"
                role="tab" aria-controls="pills-contact" aria-selected="false"><i class="fa fa-line-chart"
                  aria-hidden="true"></i>&nbsp;Report</button>
            </li>
          </ul>
          <div class="tab-content" id="pills-tabContent">
            <div class="tab-pane fade fz15 text show active" id="pills-home" role="tabpanel"
              aria-labelledby="pills-home-tab">

              <section class="breadcumb-section pt-2 pb">
                <div
                  class="cta-service-v1 freelancer-single-style mx-auto maxw1700 pt120 pt60-sm pb120 pb60-sm bdrs16 position-relative overflow-hidden d-flex align-items-center mx20-lg px30-lg">
                  <img class="left-top-img wow zoomIn" src="/images/vector-img/left-top.png" alt="">
                  <img class="right-bottom-img wow zoomIn" src="/images/vector-img/right-bottom.png" alt="">
                  <div class="container">
                    <div class="row wow fadeInUp">
                      <div class="col-xl-7">
                        <div class="position-relative">
                          <!-- <h2>I will design website UI UX in adobe xd or figma</h2> -->
                          <div class="list-meta d-flex align-items-center mt30">
                            <a class="position-relative freelancer-single-style me-1" href="#">
                              <span class="online"></span>

                              <img class=" wa-sm mb15-sm rounded-circle profile_" 
                                :src="profileLogo || '/blank_user.jpg'" alt="">

                            </a>
                            <div class="ml20 ml0-xs pro_details">
                              <h5 class="title  mb-1">{{ name }} <b><u>Buyer</u></b></h5>
                              <p class="mb-0">{{ profName }}</p>
                              <!-- <p class="mb-0 dark-color fz15 fw500 list-inline-item mb5-sm d-none">
                                <i class="fas fa-star vam fz10 review-color me-2"></i>
                                0
                                reviews
                              </p> -->
                              <p class="mb-0 me-2 dark-color fz15 fw500 list-inline-item mb5-sm ml0-xs">
                                <i class="flaticon-place vam fz20 me-2"></i>
                                {{ countryName }}
                              </p>
                              <p class="mb-0 dark-color _date fz15 fw500 list-inline-item ml15 mb5-sm ml0-xs">
                                <i class="flaticon-30-days vam fz20 me-2"></i>
                                Join : {{ joindate }}
                              </p>

                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </section>
              <div class="alert alert-success alert-dismissible fade show" role="alert">
                  {{ msgData.name }}<br />
                  {{ msgData.messages }}<br />
                  {{ msgData.created_at }}<br />

                  <div align="right">
                    <nuxt-link to="/dashboard/buyer/notificationBox">View More...</nuxt-link>
                  </div>
                </div>


              <!-- Service Details -->
              <section class="pt10 pb90">
                <div class="container">
                  <div class="row wow fadeInUp">
                    <div class="col-lg-4">
                      <h3 class="title_balence"> Available Balance: ${{ currentBalance }}</h3>

                      <center><span>Messages List</span></center>
                      <div v-if="chatUsers.length">
                        <ul class="list-group">
                          <li v-for="user in chatUsers" :key="user.id" @click="selectUser(user)"
                            class="list-group-item chat-user-item">
                            <img :src="user.profilePicture || '/about-17.png'" alt="" class="rounded-circle me-2"
                              style="width: 40px; height: 40px;" />
                            <a :href="`/dashboard/buyer/chatbox/${user.user_id}`"
                              class="text-decoration-none text-dark">
                              {{ user.user_name }}
                            </a>
                            <span class="badge bg-danger ms-1" v-if="user.unread_count > 0">{{ user.unread_count
                              }}</span>
                            <!-- Unread count -->
                          </li>
                        </ul>
                      </div>
                      <hr />
                      <ShareProfileLinkBuyer />

                      <h4 class="widget-title  title_balence">My Skills</h4>
                      <div class="tag-list mt30">
                        <a v-for="(skill, index) in skillsdata" :key="index" href="#">{{ skill.name }}</a>
                      </div>

                      <hr class="opacity-100">

                      <!-- ============{{ userResponseData . profile_status }}======== -->
                      <div class="service-about">
                        <h4 class="title_balence">Description</h4>
                        <p class="text mb30 text-justify" style="text-align: justify;">
                          {{ introduce_yourself }}</p>

                      </div>
                    </div>

                    <!-- Start -->

                    <div class="col-lg-8">

                
                      <!-- <div class="alert alert-success alert-dismissible fade show" role="alert">
                        {{ usermsgData.name }}<br />
                        {{ usermsgData.messages }}<br />
                        {{ usermsgData.created_at }}<br />
                        <div align="right">
                          <nuxt-link to="/dashboard/buyer/notidificationBox">View More...</nuxt-link>
                        </div>
                      </div> -->



                      <div class="custom-tab-container">
                        <!-- Custom Nav Tabs -->
                        <ul class="custom-nav-tabs nav nav-tabs" id="orderTabs" role="tablist">
                          <li class="custom-tab-item nav-item" role="presentation" @click="getOrderStatus(1)">
                            <a class="custom-tab-link nav-link active" id="new-order-tab" data-bs-toggle="tab"
                              href="#new-order" role="tab" aria-controls="new-order" aria-selected="true">
                              Place Order
                              <span class="badge bg-primary" style="position: absolute; top: 0; right: 0;">{{
                                placeOrdersCount }}</span>
                            </a>
                          </li>
                          <li class="custom-tab-item nav-item" role="presentation">
                            <a class="custom-tab-link nav-link" id="inprogress-tab" @click="getOrderStatus(2)"
                              data-bs-toggle="tab" href="#inprogress" role="tab" aria-controls="inprogress"
                              aria-selected="false">
                              In Progress
                              <span class="badge bg-primary" style="position: absolute; top: 0; right: 0;">{{
                                inprogressOrdersCount }}</span>
                            </a>
                          </li>
                          <li class="custom-tab-item nav-item" role="presentation">
                            <a class="custom-tab-link nav-link" id="cancel-tab" data-bs-toggle="tab" href="#cancel"
                              @click="getOrderStatus(3)" role="tab" aria-controls="cancel" aria-selected="false">
                              Cancel
                              <span class="badge bg-primary" style="position: absolute; top: 0; right: 0;">{{
                                cancelOrdersCount }}</span>
                            </a>
                          </li>
                          <li class="custom-tab-item nav-item" role="presentation">
                            <a class="custom-tab-link nav-link" id="delivery-tab" data-bs-toggle="tab" href="#delivery"
                              @click="getOrderStatus(4)" role="tab" aria-controls="delivery" aria-selected="false">
                              Delivered
                              <span class="badge bg-primary" style="position: absolute; top: 0; right: 0;">{{
                                deliveryOrdersCount }}</span>
                            </a>
                          </li>

                          <li class="custom-tab-item nav-item" role="presentation">
                            <a class="custom-tab-link nav-link" id="complete-tab" data-bs-toggle="tab" href="#complete"
                              @click="getOrderStatus(5)" role="tab" aria-controls="complete" aria-selected="false">
                              Complete
                              <span class="badge bg-primary" style="position: absolute; top: 0; right: 0;">{{
                                completeOrdersCount }}</span>
                            </a>
                          </li>
                        </ul>

                        <!-- Custom Tab Content complete -->
                        <div class="tab-content" id="orderTabContent">
                          <div class="tab-pane fade show active" id="new-order" role="tabpanel"
                            aria-labelledby="new-order-tab">
                            <div class="">
                              <div class="table-responsive">
                                <table class="table table-bordered table-hover">
                                  <thead class="thead-dark">
                                    <tr>
                                      <th scope="col">Order ID</th>
                                      <th scope="col">Gig Title</th>
                                      <th scope="col">
                                        <center>Date</center>
                                      </th>
                                      <!-- <th scope="col">Action</th>  -->
                                    </tr>
                                  </thead>
                                  <tbody>
                                    <tr v-for="(order, index) in orderData" :key="index">
                                      <td>#{{ order.orderId }}</td>
                                      <td><nuxt-link :to="`/gigs/${order.gig_slug}`">{{ order.gig_name }}
                                          Price:
                                          ${{ order.selected_price }}</nuxt-link>
                                      </td>
                                      <td class="text-center">
                                        {{ formatDate(order.created_at) }}</td>
                                      <!-- <td>
                                        <button class="btn btn-success btn-sm text-white me-2"
                                          @click="acceptMyOrders(order.orderId)">Accept</button>
                                        <button class="btn btn-danger btn-sm text-white"
                                          @click="rejectOrders(order.orderId)">Cancel</button>
                                      </td> -->
                                    </tr>

                                  </tbody>
                                </table>

                              </div>
                            </div>

                          </div>
                          <div class="tab-pane fade" id="inprogress" role="tabpanel" aria-labelledby="inprogress-tab">
                            <!-- <p>Custom Content for In Progress.</p> -->

                            <div class="table-responsive">
                              <table class="table table-bordered table-hover">
                                <thead class="thead-dark">
                                  <tr>
                                    <th scope="col">Order ID & Date</th>
                                    <th scope="col">Gig Title</th>
                                    <th scope="col">
                                      <center>Reaming Time</center>
                                    </th>
                                    <th scope="col">Action</th>
                                    <!-- Action Column -->
                                  </tr>
                                </thead>
                                <tbody>
                                  <tr v-for="(order, index) in inprogressData" :key="index">
                                    <td>#{{ order.orderId }}<br />{{ formatDate(order.created_at) }}
                                    </td>
                                    <td><nuxt-link :to="`/gigs/${order.gig_slug}`">{{ order.gig_name }}
                                        Price:
                                        ${{ order.selected_price }}</nuxt-link>
                                    </td>
                                    <td class="text-center" v-html="order.reamingitime"></td>
                                    <td>

                                      <div class="btn-group" role="group" aria-label="Basic example">
                                        <nuxt-link :to="`/dashboard/buyer/orderDetails/${order.orderId}`"
                                          class="btn-sm btn btn-primary text-white">Details</nuxt-link>
                                        <nuxt-link :to="`#`" class="btn-sm btn btn-danger text-white"
                                          @click="cancelOrders(order.orderId)">Cancel</nuxt-link>
                                      </div>
                                      <!-- <button class="btn btn-primary btn-sm text-white" @click="rejectOrders(order.orderId)">Details</button> -->
                                    </td>
                                  </tr>

                                </tbody>
                              </table>

                            </div>
                          </div>
                          <div class="tab-pane fade" id="cancel" role="tabpanel" aria-labelledby="cancel-tab">
                            <!-- <p>Custom Content for Cancel.</p> -->

                            <div class="table-responsive">
                              <table class="table table-bordered table-hover">
                                <thead class="thead-dark">
                                  <tr>
                                    <th scope="col">Order ID</th>
                                    <th scope="col">Gig Title</th>
                                    <th scope="col">
                                      <center>Date</center>
                                    </th>
                                    <th scope="col">Status</th>
                                    <!-- Action Column -->
                                  </tr>
                                </thead>
                                <tbody>
                                  <tr v-for="(order, index) in cancelData" :key="index">
                                    <td>#{{ order.orderId }}</td>
                                    <td><nuxt-link :to="`/gigs/${order.gig_slug}`">{{ order.gig_name }}
                                        Price:
                                        ${{ order.selected_price }}</nuxt-link>
                                    </td>
                                    <td class="text-center">
                                      {{ formatDate(order.created_at) }}</td>
                                    <td class="text-danger text-center">Canceled
                                      <br />[{{ order.cancel_resion }}]
                                    </td>
                                  </tr>

                                </tbody>
                              </table>

                            </div>
                          </div>
                          <div class="tab-pane fade" id="delivery" role="tabpanel" aria-labelledby="delivery-tab">
                            <!-- <p>Custom Content for Delivery.</p> -->

                            <div class="table-responsive">
                              <table class="table table-bordered table-hover">
                                <thead class="thead-dark">
                                  <tr>
                                    <th scope="col">Order ID</th>
                                    <th scope="col">Gig Title</th>
                                    <th scope="col">
                                      <center>Date</center>
                                    </th>
                                    <th scope="col">Action</th>
                                    <!-- Action Column -->
                                  </tr>
                                </thead>
                                <tbody>
                                  <tr v-for="(order, index) in deliveryData" :key="index">
                                    <td>#{{ order.orderId }}</td>
                                    <td><nuxt-link :to="`/gigs/${order.gig_slug}`">{{ order.gig_name }}
                                        Price:
                                        ${{ order.selected_price }}</nuxt-link>
                                    </td>
                                    <td class="text-center">
                                      {{ formatDate(order.created_at) }}</td>
                                    <td>
                                      <nuxt-link :to="`/dashboard/buyer/orderDetails/${order.orderId}`"
                                        class="btn-sm btn btn-primary text-white">Details</nuxt-link>
                                    </td>
                                  </tr>

                                </tbody>
                              </table>

                            </div>

                          </div>

                          <div class="tab-pane fade" id="complete" role="tabpanel" aria-labelledby="complete-tab">
                            <!-- <p>Custom Content for Delivery.</p> -->

                            <div class="table-responsive">
                              <table class="table table-bordered table-hover">
                                <thead class="thead-dark">
                                  <tr>
                                    <th scope="col">Order ID</th>
                                    <th scope="col">Gig Title</th>
                                    <th scope="col">
                                      <center>Date</center>
                                    </th>
                                    <th scope="col">Action</th>
                                    <!-- Action Column -->
                                  </tr>
                                </thead>
                                <tbody>
                                  <tr v-for="(order, index) in completeData" :key="index">
                                    <td>#{{ order.orderId }}</td>
                                    <td><nuxt-link :to="`/gigs/${order.gig_slug}`">{{ order.gig_name }}
                                        Price:
                                        ${{ order.selected_price }}</nuxt-link>
                                    </td>
                                    <td class="text-center">
                                      {{ formatDate(order.created_at) }}</td>
                                    <td>
                                      <nuxt-link :to="`/dashboard/buyer/orderDetails/${order.orderId}`"
                                        class="btn-sm btn btn-primary text-white">Details</nuxt-link>
                                    </td>
                                  </tr>

                                </tbody>
                              </table>

                            </div>

                          </div>
                        </div>
                      </div>

                      <!-- <center><button class="btn btn-primary" @click=getwhislistData>Test</button></center> -->
                      <!-- <nuxt-link :to="`/gigs/${data.gig_slug}`">{{ data.name || '' }} </nuxt-link> -->
                      <div class="row">
                        <center>
                          <p>Wish List</p>
                        </center>
                        <div class="col-sm-6 col-xl-4" v-for="gig in gigData" :key="gig.id">
                          <div class="listing-style1">
                            <div class="list-thumb">
                              <!-- Delete -->
                              <nuxt-link :to="`/gigs/${gig.gig_slug}`" ><img class="w-100" :src="gig.thumbnail_images" alt="">
                              <a href="#" class="listing-fav fz12" @click="deleteGig(gig.id)"><i
                                  class="fa-solid fa-trash"></i></a></nuxt-link>
                              <!-- Share  -->
                              <nuxt-link :to="`/gigs/${gig.gig_slug}`" @click="shareUrl(gig.gig_slug)"
                                class="listing-fav fz12" style="left: 20px;">
                                <i class="fa-solid fa-share"></i>
                              </nuxt-link>

                              <!-- Edit  -->
                            </div>

                          </div>
                        </div>
                      </div>

                    </div>

                  </div>
                </div>
              </section>

            </div>

            <!-- Modal -->
            <!-- Modal -->
            <div class="modal fade" id="myModal_cancel" tabindex="-1" aria-labelledby="myModal_cancelLabel"
              aria-hidden="true">
              <div class="modal-dialog modal-dialog-centered" role="document">
                <div class="modal-content">
                  <div class="modal-header">
                    <h5 class="modal-title" id="myModal_cancelLabel">Cancel Order</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                  </div>
                  <div class="modal-body">
                    <!-- Cancel Order Form -->
                    <form @submit.prevent="submitCancelOrder">
                      <div class="mb-3">
                        <label for="cancelReason" class="form-label">Reason for
                          Cancellation</label>
                        <textarea v-model="cancelReason" id="cancelReason" class="form-control" rows="4"
                          placeholder="Please explain why you want to cancel the order"></textarea>
                      </div>
                      <p v-if="errorMessage" class="text-danger">{{ errorMessage }}</p>
                    </form>
                  </div>
                  <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-primary text-white" @click="submitCancelOrder">Submit
                      Cancellation</button>
                  </div>
                </div>
              </div>
            </div>

            <!-- END -->

          </div>
        </div>

      </div>

      <!-- <div class="tab-pane fade fz15 text" id="pills-contact" role="tabpanel" aria-labelledby="pills-contact-tab"></div> -->
    </div>
  </div>

</template>

<script setup>
import {
  useRoute
} from 'vue-router';
import axios from 'axios';

import {
  useRouter
} from 'vue-router';
import Swal from "sweetalert2";
const euddata = ref([]);
const chatUsers = ref([]);
const expdata = ref([]);
const certificatedata = ref([]);
const router = useRouter();
const name = ref('');
const joindate = ref('');
const usermsgData = ref([]);
const countryName = ref('');
const profName = ref('');
const introduce_yourself = ref('');
const profileLogo = ref('');
const skillsdata = ref('');
const loading = ref(false);
const route = useRoute();
const orderData = ref('');
const currentBalance = ref(0);
const cancelReason = ref('');

definePageMeta({
  middleware: "is-logged-out",
});

const profileModal = ref(null);
const msgData = ref([]);

const gigData = ref([]);
const getwhislistData = async () => {
  try {
    const response = await axios.get(`/gig/getwishListGig`);
    gigData.value = response.data;
  } catch (error) {
    console.log(error);
  }
};

const getMessages = async () => {
  try {
    const response = await axios.get(`/user/getMessagesNoti`);
    msgData.value = response.data;
  } catch (error) {
    console.log(error);
  }
};

const deleteGig = async (id) => {
  // Show confirmation dialog
  const result = await Swal.fire({
    title: 'Are you sure?',
    text: "You won't be able to revert this!",
    icon: 'warning',
    showCancelButton: true,
    confirmButtonColor: '#3085d6',
    cancelButtonColor: '#d33',
    confirmButtonText: 'Yes, delete it!'
  });

  // Check if the user confirmed
  if (result.isConfirmed) {
    try {
      const response = await axios.get('/gig/deleteWishListGig', {
        params: { id: id }
      });

      // Call gigList function after successful deletion
      if (response.status === 200) {

        Swal.fire(
          'Deleted!',
          'Your gig has been deleted.',
          'success'
        );
        getwhislistData();
      }
    } catch (error) {
      console.log(error);
      Swal.fire(
        'Error!',
        'There was an error deleting your gig.',
        'error'
      );
    }
  }
};

const selectUser = (users) => {
  const userId = users.user_id; // Get user_id from reactive data
  const currentUrl = window.location.origin; // Get current origin (e.g., http://example.com)
  const fullUrl = `${currentUrl}/dashboard/buyer/chatbox/${userId}`; // Construct the full URL
  window.location.href = fullUrl;
}

const getChatusersList = async () => {
  try {
    const response = await axios.get(`/chat/getChatUsers`);
    chatUsers.value = response.data;
  } catch (error) {
    // Handle error
  }
};
const shareUrl = (slug) => {
  const currentUrl = window.location.origin; // Get the base URL (e.g., https://example.com)
  const fullUrl = `${currentUrl}/gigs/${slug}`; // Construct the full URL with slug

  navigator.clipboard.writeText(fullUrl)
    .then(() => {

      Swal.fire(
        'Copied!',
        'Your gig URL has been copied.',
        'success'
      );

      //alert('URL copied to clipboard!');
    })
    .catch(err => {
      console.error('Failed to copy URL: ', err);
    });
};

const submitCancelOrder = () => {
  //console.log("============orderId:" + canceOrderID.value);
  //console.log("============cancelReason:" + cancelReason.value);
  // Show the confirmation alert before proceeding
  Swal.fire({
    title: 'Are you sure?',
    text: 'Do you want to cancel this order?',
    icon: 'warning',
    showCancelButton: true,
    confirmButtonColor: '#3085d6',
    cancelButtonColor: '#d33',
    confirmButtonText: 'Yes, cancel it!',
    cancelButtonText: 'No, keep it'
  }).then((result) => {
    if (result.isConfirmed) {
      // If user confirms, send the cancel request
      axios.get('/order/cancel-order-buyer', {
        params: {
          orderId: canceOrderID.value,
          cancel_resion: cancelReason.value
        }
      })
        .then(response => {
          // Handle the response (success or failure)
          Swal.fire(
            'Cancelled!',
            'Your order has been cancelled.',
            'success'
          );
        })
        .catch(error => {
          // Handle errors
          Swal.fire(
            'Error!',
            'There was an issue cancelling your order. Please try again.',
            'error'
          );
        });
    }
  });
}

const canceOrderID = ref("");
const cancelOrders = (orderId) => {
  canceOrderID.value = orderId;
  $('#myModal_cancel').modal('show');

}

const chkUserrow = async () => {
  try {
    const response = await axios.post(`/auth/me`);
    //console.log("Profile Status: ", response.data.profile_status);
    name.value = response.data.name;
    joindate.value = response.data.joindate;
    countryName.value = response.data.countryName;
    profName.value = response.data.profName;
    introduce_yourself.value = response.data.introduce_yourself
    profileLogo.value = response.data.profileLogo;

  } catch (error) {
    console.error("Error fetching user data:", error);
  }
};

const myprofile = () => {
  router.push('/dashboard/buyer/myprofile')
}

const chatbox = () => {
  router.push('/dashboard/buyer/chatbox')
}

const mysetting = () => {
  router.push('/dashboard/buyer/setting')
}
const myorders = () => {
  router.push('/dashboard/buyer/orders')
}
const deposit = () => {
  router.push('/dashboard/buyer/deposit')
}

const mywithdraw = () => {
  router.push('/dashboard/buyer/withdrawalrequest')
}

const mlm = () => {
  router.push('/dashboard/buyer/mlm')
}

const getBalance = async () => {
  try {
    const response = await axios.get(`/user/checkBalance`);
    currentBalance.value = response.data.currentBalance;
  } catch (error) {
    console.log(error);
  }
};
const getUsersMessages = async () => {
  try {
    const response = await axios.get(`/user/getMessagesUserWisebuyer`);
    usermsgData.value = response.data;
  } catch (error) {
    console.log(error);
  }
};

const getMessagesNotif = async () => {
  try {
    const response = await axios.get(`/user/getMessagesNoti`);
    msgData.value = response.data;
  } catch (error) {
    console.log(error);
  }
};



const getAllOrdersList = async () => {
  try {
    const response = await axios.get(`/order/getOrderPlace`);
    orderData.value = response.data;
  } catch (error) {
    console.log(error);
  }
};

// Function to format the date
const formatDate = (date) => {
  const options = {
    year: 'numeric',
    month: 'long',
    day: 'numeric'
  };
  return new Date(date).toLocaleDateString(undefined, options);
};

let intervalId = null;
intervalId = setInterval(getAllOrdersList, 10000); // Set interval for 10 seconds

const inprogressData = ref([]);
const cancelData = ref([]);
const deliveryData = ref([]);
const completeData = ref([]);
const placeOrdersCount = ref(0);
const inprogressOrdersCount = ref(0);
const deliveryOrdersCount = ref(0);
const cancelOrdersCount = ref(0);
const completeOrdersCount = ref(0);

const getOrderCounting = async () => {
  try {
    const response = await axios.get(`/order/getOrderCountBuyer`);
    placeOrdersCount.value = response.data.placeOrdersCount;
    inprogressOrdersCount.value = response.data.inprogressOrdersCount;
    cancelOrdersCount.value = response.data.cancelOrdersCount;
    deliveryOrdersCount.value = response.data.deliveryOrdersCount;
    completeOrdersCount.value = response.data.completeOrdersCount;

  } catch (error) {
    console.log(error);
  }
};

const getOrderStatus = async (orderStatusId = 1) => {
  try {
    const response = await axios.get(`/order/getOrderPlaceForByer`, {
      params: {
        orderStatusId
      } // Passing orderStatusId as a query parameter
    });

    if (orderStatusId = 1) {
      orderData.value = response.data.placeOrders;
    }

    if (orderStatusId = 2) {
      inprogressData.value = response.data.inprogressOrders;

    }
    if (orderStatusId = 3) {
      cancelData.value = response.data.cancelOrders;
    }

    if (orderStatusId = 4) {
      deliveryData.value = response.data.deliveryOrders;
    }

    if (orderStatusId = 5) {
      completeData.value = response.data.completeOrders;
    }

    getOrderCounting();

  } catch (error) {
    console.log(error);
  }
};

onMounted(() => {
  getUsersMessages();
  getwhislistData();
  getChatusersList();
  getMessages();
  getBalance();
  getOrderCounting();
  getOrderStatus();
  getAllOrdersList();
  chkUserrow();
  getMessagesNotif();
});
onBeforeUnmount(() => {
  clearInterval(intervalId); // Clear interval when component is unmounted
});
</script>
<style scoped>
.chat-user-item {
  cursor: pointer;
  /* Change cursor to pointer */
  transition: background-color 0.3s;
  /* Smooth background transition */
}

.chat-user-item:hover {
  background-color: #f8f9fa;
  /* Light gray on hover */
}

.chat-user-item.selected {
  background-color: #e0e0e0;
  /* Background for selected user */
  font-weight: bold;
  /* Bold text for selected user */
}

.order-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 20px;
}

.card {
  width: calc(50% - 15px);
  margin-bottom: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s, box-shadow 0.3s;
  background-color: #ffffff;
}

.chat-user-item {
  cursor: pointer;
}

.card:hover {
  transform: translateY(-5px);
  /* Lift the card on hover */
  box-shadow: 0 6px 30px rgba(0, 0, 0, 0.2);
  /* Deeper shadow on hover */
}

.card-header {
  font-weight: bold;
  /* Bold text for order ID */
  background-color: #f8f9fa;
  /* Light gray background for header */
  border-top-left-radius: 10px;
  /* Round top left corner */
  border-top-right-radius: 10px;
  /* Round top right corner */
}

.card-body {
  padding: 15px;
  /* Add padding inside the card body */
}

.card-title {
  font-size: 1.2em;
  /* Increase font size for title */
  color: #007bff;
  /* Primary color for title */
}

.card-text {
  font-size: 0.9em;
  /* Slightly smaller text for details */
  color: #555;
  /* Darker gray for text */
}

.card-footer {
  background-color: #f8f9fa;
  /* Light gray background for footer */
  border-bottom-left-radius: 10px;
  /* Round bottom left corner */
  border-bottom-right-radius: 10px;
  /* Round bottom right corner */
}

.btn-primary {
  background-color: #007bff;
  border: none;
}

.btn-primary:hover {
  background-color: #0056b3;
  /* Darker blue on hover */
}

.categories_list_section {
  border-bottom: 1px solid #E9E9E9;
  padding: 7px 0 3px;
  position: relative;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* Custom Tab Container */
.custom-tab-container {
  background-color: #f9f9f9;
  border-radius: 10px;
  width: 100%
}

/* Custom Tab Links */
.custom-nav-tabs {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
  padding: 0;
  list-style: none;
  border-bottom: 2px solid #ccc;
}

.custom-tab-item {
  flex: 1;
  text-align: center;
}

.custom-tab-link {
  display: block;
  padding: 10px 0;
  font-size: 16px;
  font-weight: 500;
  color: #555;
  background-color: #e9ecef;
  text-decoration: none;
  border-radius: 5px 5px 0 0;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.custom-tab-link:hover,
.custom-tab-link:focus {
  background-color: #185a48;
  color: #333;
}

.custom-tab-link.active {
  background-color: #1f4b3f;
  color: white;
  border-bottom: 3px solid #fff;
}

/* Custom Tab Content */
.tab-pane {
  padding: 10px;
  background-color: white;
  border-radius: 0 0 5px 5px;
  box-shadow: 0 2px 4px rgba(119, 118, 118, 0.1);
}

/* Responsive Tabs */
@media (max-width: 767px) {
  .custom-nav-tabs {
    width: 100%;
    overflow: auto;
    display: grid;
    grid-template-columns: repeat(3,3fr);
  }

  .custom-tab-item {
    margin-bottom: 10px;
  }
}

.custom-tab-link {
  position: relative;
  /* Add relative positioning to the link */
}

.badge {
  position: absolute;
  /* Position the badge absolutely */
  top: 0;
  /* Adjust the vertical position */
  right: 0;
  /* Adjust the horizontal position */
}

.table-responsive {
  max-width: 100%;
  overflow-x: auto;
}
@media(max-width: 576px){
  .custom-tab-link{
  display: block;
  padding: 10px 0;
  font-size: 14px;
  }
}
</style>
