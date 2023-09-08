# # FROM tensorflow/tensorflow:2.5.1 as builder
# FROM armswdev/tensorflow-arm-neoverse:latest as builder


# ARG SERVER_DIR=imagenet_inception_v3
# ENV PROJECT_DIR synchronous pattern

# COPY . .
# WORKDIR /${PROJECT_DIR}
# ADD ./${SERVER_DIR}/requirements.txt /${PROJECT_DIR}/
# RUN pip install --no-cache-dir -r requirements.txt && \
#     touch __init__.py

# # apt-get -y update && \
#     # apt-get -y install apt-utils gcc && \
# # apt-get clean && \
# # rm -rf /var/lib/apt/lists/* && \

# COPY ./${SERVER_DIR}/extract_inception_v3.py /${PROJECT_DIR}/extract_inception_v3.py
# COPY ./${SERVER_DIR}/image_net_labels.json /${PROJECT_DIR}/image_net_labels.json

# RUN python -m extract_inception_v3

FROM emacski/tensorflow-serving:latest
# tensorflow/serving:2.5.2


ARG SERVER_DIR=imagenet_inception_v3
ENV PROJECT_DIR synchronous_pattern
ENV MODEL_BASE_PATH /${PROJECT_DIR}/saved_model/inception_v3
ENV MODEL_NAME inception_v3

# --from=builder
# COPY --from=builder /synchronous_pattern/saved_model/inception_v3 ${MODEL_BASE_PATH}
COPY ./${SERVER_DIR}/saved_model/inception_v3/ ./{MODEL_NAME}
COPY /${SERVER_DIR}/tf_serving_entrypoint.sh /usr/bin/tf_serving_entrypoint.sh
EXPOSE 8500
EXPOSE 8501

COPY ./${SERVER_DIR}/tf_serving_entrypoint.sh /usr/bin/tf_serving_entrypoint.sh
RUN /bin/chmod +x /usr/bin/tf_serving_entrypoint.sh
ENTRYPOINT ["/usr/bin/tf_serving_entrypoint.sh"]