<script>
export default {
    props: {
        reader: { type: Object, required: true },
    },
};
</script>

<template>
    <div class="row">
        <div class="col-md-6">
            <div class="p-2">
                <strong>Họ và tên:</strong>
                {{ reader.HOLOT }} {{ reader.TEN }}
            </div>
            <!-- Display other reader details accordingly -->
        </div>

        <div class="col-md-6">
            <!-- Add image display or any other details here -->
        </div>
    </div>

</template>
